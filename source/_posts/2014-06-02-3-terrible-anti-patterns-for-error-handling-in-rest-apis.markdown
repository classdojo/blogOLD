---
layout: post
title: "3 Terrible Anti-patterns for Error-Handling in 'REST' APIs:"
date: 2013-04-21 22:22:07 -0700
comments: true
categories: apis, rest, http
---

I’ve seen these anti-patterns in a lot of web APIs, so I thought I’d detail why they’re bad and what to do instead.

# Using a 200 status code for every response:
This anti-pattern is common for SOAP-like RPC APIs.  Using a 200 status code for all your responses is silly because you end up having to reinvent an error-indication in your response body instead, and nobody in the world knows your new standard (or wants to have to learn it).

It’s also extremely confusing in the cases that an error has occurred because a status code of 200 means everything is A-OK.  [There are already a bunch of error codes in the 400 and 500 ranges](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) that are fully capable of indicating all sorts of common problems. It’s still great to put an error message in the response body, but there should be a 400 or 500-level status code so people know that an error even occurred and don’t go ahead and try to interpret the response body as normal or otherwise assume a success.

# Using a 500 status code for all errors:
This anti-pattern is common because 500 is what most frameworks will do when a web application throws an uncaught exception, and so it becomes convenient to just throw exceptions and not worry about the repercussions. This is mildly better than using a 200 status code for literally everything, because at least it shows an error occurred but it still causes a lot of confusion for client developers.

When you 500 for an error (even if your web framework did it for you), you’re signalling that the problem with the request was the fault of your application (the server) and it’s possible that retrying the request will be successful. Because 500 errors indicate an internal **server error**, they shouldn’t actually ever happen though[^1] — In general, you’ve got a bug in your application if they do, and the web server will tell everyone about it. The right thing to do, if there’s something wrong with the request is to respond with the appropriate 400-level status code.

Using a 500 error when a 400-level status code is more appropriate is obviously really confusing to the person making the requests because it doesn’t even let them know that their request needs to be fixed. Even if that person is also you, it forces you to start digging into your back-end for what could possibly just be a bad client request. If you don’t know which 400-level code to use, at the very least use 400 (Bad Request) itself. This will at least give your client developer an indication if the blame is on the server or the client and cut your debugging in half. A few words about the error in the response body can go a long way as well.

# Logging 400-level codes at ‘error’ level:
Logging is pretty important to measuring the quality of implementation of an API, and learning about specific defects. The ‘error’ level in your logs should be a way to indicate “things that should not have happened that are within this application’s control”, so that you actually have a hope of attempting a 0-error policy. 400 level codes are errors of course, but they’re client errors, and not your server application’s error, so they should not be logged as errors along with your actual 500-level errors (Of course you might still log them as “info” level to keep track of what kinds of crazy things your clients are doing).

# Why do all these details matter?
When you have an interface between two applications (the client and the server in this case) like HTTP, it REALLY simplifies things a lot if they communicate whether messages are acceptable or not (and why). Even if you control both ends of the interaction, you can save yourself a lot of server-side debugging by having the server indicate what exactly went wrong with a given request, instead of repeatedly reading stack traces every time some JSON you POSTed is missing a property. Compared to how little extra work there is involved in communicating the problem correctly, it’s pretty short-sighted to just let all exceptions bubble-up, or catch all exceptions silently (and 200).

Keep in mind too that if you’re now convinced that communicating errors is important, then HTTP already has a system for just that: HTTP status codes (plus whatever specifics you want to additionally communicate in the response body). Status codes are part of the greater HTTP standard that a lot of developers, libraries, proxies, and caches already understand. Re-inventing your own error mechanism is generally a waste of everyone’s time (with you at the top of the list).

Getting this right is a real time-saver over the long-haul even if you’re the only consumer of the API writing both client-side and server-side.  The time-savings only multiplies as you add more clients.

[^1]: Sometimes 500 is appropriate of course: If your application requires a database and its lost connectivity to it, then a 500 makes total sense. It signals that there’s a problem in your application and the client can possibly try the request again later.
