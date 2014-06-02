---
layout: post
title: "Production-Quality Node.js Web Apps : Part I, The Basics"
date: 2014-06-01 10:09:00 -0700
comments: true
sharing: true
footer: true
categories: programming, node.js, quality 
---

I've been working on production-quality node.js web applications for a couple of years now, and I thought it'd be worth writing down some of the more interesting tricks that I've learned along the way.

I'm mostly going to talk about maintaining a low-defect rate and high availability, rather than get into the details about scaling that are covered in a lot of other places.   In particular, I’ll be talking about load-balancing, process management, logging, and metrics, and the how’s and why’s of each.


### Balance the Load
I'm going to assume that you're already load-balancing on a given server with [cluster](http://nodejs.org/api/cluster.html) or some higher level abstraction ( I use [cluster-master](https://github.com/isaacs/cluster-master)) as well as between servers with a load-balancer like [ha-proxy](http://haproxy.1wt.eu/).

Performance considerations aside, your service will have much better availability, quality, and uptime if you've got multiple processes running on multiple machines.  More specifically, you get:
* the ability to immediately failover in the case of single process or single machine failure
* reduced overall service failure in the case of single process or single machine failure 
* the ability to gracefully deploy with the load-balancer

### Gracefully Deploy
Gracefully deploying means that your deploy process has enough servers running to handle the load at all times throughout the actual deployment process, and that none of the servers are taken off-line while outstanding requests are still in progress.  This means:

 
* Your clustering solution must be able to stop new connections and not exit the master process until all servers have finished processing their existing requests.  The solution I personally use is [cluster-master](https://github.com/isaacs/cluster-master), but there are bunch of suitable alternatives.

* You need a rolling deployment, meaning that servers are restarted one-at-a-time, or in small groups, rather than all at once.  The easiest way to do this is probably to write a nice deploy script that takes restarting servers out of the load-balancer until they're running again.

If you don't have a graceful deploy solution, every deployment of new code will lose requests in progress, and your users will have a terrible experience.

Also note: I've seen a few clustering solutions that use some sort of hot-deploy (hot-deploy loads a new version of code without taking the server down) functionality.  If you've got a rolling deploy via your load balancer though, you probably *don't* need any sort of hot-deploy functionality.  I'd personally avoid solutions that involve the complexity of hot-deploying.

### Run as a Service 
You're also going to want to be running your app as a service that the OS knows to restart with some service manager like [upstart](http://caolanmcmahon.com/posts/deploying_node_js_with_upstart/).  A service manager like this is going to be absolutely essentially for when your node.js app crashes, or when you spin up new machines.

It's probably worth noting that you won't really want to use something like [forever](https://github.com/nodejitsu/forever) or [nodemon](http://nodemon.io/) in production, because it doesn't survive reboots, and is pretty redundant once you've added service management that actually does (This is a case where you don't want redundancy, because these types of process managers can end up fighting with each other to restart the app, thus never really allowing the app to start).


#### Log to Standard Output
Logging to standard output (using `console.log()`) and standard error (using `console.error()`) is the simplest and most powerful way to log.  Here's how:  

##### pipe it, don't write it
In the config file for running your app, you want something like this to specify a log file:

```bash
node server.js >> /var/log/myserver.log 2>&1
```  

The `>>` tells your node process to append output to the specified log file and the `2>&1` tells it that both standard out and standard error should go to that same log file.  You don't want to be writing to the logs programmatically from within the node process, because you will miss any output that you don't specifically log, like standard error output from node.js itself which happens anytime that your server crashes.  That kind of information is too critical to miss.  

##### console is the only "logging library" you need
With this kind of logging set up, I just have to `console.log()` for any debug output that I need (usually just temporarily for a specific issue that I'm trying to solve), or `console.error()` for any errors I encounter.

Additionally, one of the first things I do on a new web service is to set up a `console.log()` for each request (this should work in any `express` or `connect` app):

```javascript
  app.use(function(req, res, next){
    res.on('finish', function(evt){
      console.log(req.method, req.url, res.statusCode);
    });
  });
``` 

This chunk of code gives me nice simple logs for every request that look like this:

```
...
POST /api/session 400
POST /api/session 401
POST /api/session 200
GET /api/status 200
GET /api/status 200
...
```

##### rotating the logs

The missing infrastructure needed to support this is a way to rotate the logs, like [logrotate](http://www.rackspace.com/knowledge_center/article/understanding-logrotate-part-1).  Once that's set up properly, your logs will rotate for you nicely and not fill up your disk on you.

## Tools to Help Detect Problems at Runtime

There are two basic key ways that I like to instrument an application to detect problems that occur at runtime: Aggregated logging and metrics.

#### Agreggated Logging
One of the most important things you can do for error and defect detection is to have aggregated logging -- some service that brings all your web servers' logs together into one large searchable log.  There are a few products for this:  The stand-out open source one for me seemed to be the [logstash/kibana combination](http://www.elasticsearch.org/overview/kibana/), though these days I'm lazy and generally use the [papertrail service](https://papertrailapp.com/) instead.

I would highly recommend that you set a service like this up immediately, because the small amount of friction involved in `ssh`ing into servers to `tail` logs is enough to seriously reduce how often you and your teammates will actually look at the logs. The sooner you set this up, the sooner you can benefit from being able to learn about your application through the logs that you have it write.

#### Metrics
When I say "metrics" I really mean time-series metrics, that allow me to see the frequency of different types of events over time.  These are invaluable because they

* tell you when something unusual is happening
* aggregate certain types of data in ways that logs can't
* help you rally the team or company around specific high-value goals (be careful with this one!)

The stand-out metrics/graphic open source product is probably [graphite](http://graphite.wikidot.com/).  I've generally been using [Librato's metrics service](https://metrics.librato.com) though because it's easy to set up, and looks great, so that's where I'll pull my screenshots from for time-series data.  I've also had a pretty good experience with [DataDog's service](http://datadog.com) as well.  Both also come with the ability to raise alerts when a metric surpasses a threshold, which can be a nice way to know when something is going on that you should investigate. 

##### Basic Metrics
There are a bunch of basic metrics that you can track to see what's going on in your server.  

Here's an example of some very high-level metrics for us over a week:

{% img /images/metrics_requests_duration.png [metrics : number of requests vs average duration [metrics : number of requests vs average duration]] %}

* in blue: number of requests
* in green: average duration of requests

(Note that at this resolution, the y-values are averages over such long durations that the values aren't really that useful at face value; it's the visualization of general trends that is useful.)

There are a few obvious things that should jump out right away in this example:

* We have daily traffic spikes with 5 peaks really standing out and 2 being almost flat (those happen to be Saturday and Sunday).
* We had a spike in average request duration (on Friday morning -- the third peak).  This was caused by some performance issues with our database, and resulted in service outage for a number of our users during that time.

I can basically put `metrics.increment("someEventName");` anywhere in my codebase to tell my metrics service when a particular event occurred.   

Also consider OS metrics like:
* disk space usage
* cpu utilization
* memory consumption
* etc, etc

I've got my codebase set up so that `metrics.gauge("someMetricName", value);` will allow me to graph specific values like these over time as well.

If you're not already doing monitoring like this, you must be wondering what your servers would tell you.  When it's this easy, you tend to do it all the time and get all kinds of interesting metrics including more business-specific metrics.

## What next?

These are really just the basics.  If you're not doing these things, and you care about running a production-quality web service, you're probably putting yourself at a disadvantage.

There is a lot more that you can do though, and I'll get into that in my next post, which will be Part II to this one.

