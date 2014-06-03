---
layout: post
title: "You probably don’t need to version your web API."
date: 2013-09-13 18:47:31 -0700
comments: true
categories: apis 
---


So you’re thinking about versioning your web API somehow.  Versioning is how we annotate and manage changes in software libraries, so it seems natural to re-apply this solution to changes in web APIs.  Most web APIs are versioned in order to…

**( A ) “freeze” an older version somehow so that it doesn’t change for older clients, or at least it is subjected to much less change than newer versions, so you can still move forward.**

**( B ) be able to deprecate older APIs that you no longer wish to support.**

**( C ) indicate that changes have occurred and represent a large batch of changes at once when communicating with others.**

## However…
**( A )  Versions don’t actually solve the problem of moving forward despite older clients.**

You can safely break backward compatibility with or without the concept of versions: just create a new endpoint and do what you want there.  It doesn’t need to have any impact on the old endpoint at all.  You don’t need the concept of “versions” to do that.

**( B ) Versions don’t actually solve the problem of deprecating old endpoints.**

At best, versions just defer the problem, while forcing you to pay the price of maintaining two sets of endpoints until you actually work out a real change management strategy.  If you have an endpoint that you want to retire, you’re going to have to communicate that to all your clients that you’re deprecating it, regardless of whether or not you’ve “versioned” it.

**( C )  Versions DO help you communicate about changes in a bunch of endpoints at once.  But you shouldn’t do this anyway.**

Of course, if you’re retiring 20 endpoints at once, it’s easier to say “we’re retiring version 1” than to say “we’re retiring the following endpoints…” (and then list all 20), but why would you want to drop 20 breaking-change notices on your clients all at once?  Tell your clients as breaking changes come up, and tell them what sort of grace period they get on those changes.  This gives you fine-grained control over your entire API, and you don’t need to think about a new version for the entire API every time you have a breaking change.  Your users can deal with changes as they occur, and not be surprised with many changes at once (your new version).

## “So how the @#$% do I manage change in my API??”
With a little imagination, it’s totally possible.  Facebook is one of the largest API providers in the world, and it doesn’t version its API.

**Take Preventative measures:**  Spend more time on design, prototyping, and beta-testing your API before you release it.  If you just throw together the quickest thing that could possibly work, you’re going to be paying the price for that for a long time to come.  An API is a user interface, and as such it needs to actually be carefully considered.

**Consider NOT making non-essential backwards-incompatible changes:** If there are changes you’d like to make in order to make your API more aesthetically-pleasing, and you can’t do so in an additive fashion, try to resist those changes entirely.  A good public-facing API should value backward compatibility very highly.

**Make additive changes when possible:** If you want to add a new property to some resource, just add it. Old clients will just ignore it.  If you want to make breaking changes to some resource, consider just creating a new resource.

**Use sensible defaults where possible:**  If you want a client to send a new property, make it optional, and give it a sensible default.

**Keep a changelog, roadmap and change-schedule for your API:**  If you want to solve the problem of keeping your users abreast of changes in your API, you need to publish those changes somehow.

**Use hypermedia:**  Tell the clients what uris to use for the requests that it needs to make and give them uri templates instead of forcing them to make their own uris.  This will make your clients much more resilient to change because it frees you up to change uris however you want.  Clients making their own uris are tomorrow’s version of parsing json with regular expressions.

## NB!

Notice that almost all of these are things that you should do regardless of whether or not you version your API, so they’re not really even extra work.

Notice also that I never said “Never make changes”.  I’m not trying to make an argument against changes.  I’m just saying that versioning doesn’t help you make changes at all.  At best it just lets you put a bunch of changes in a “bucket” to dump on your API users all at once.
