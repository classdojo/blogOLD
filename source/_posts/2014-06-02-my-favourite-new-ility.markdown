---
layout: post
title: "My Favourite New Ility"
date: 2013-06-09 21:21:46 -0700
comments: true
categories: programming
---

If you’ve ever seen a laundry list of the types of [non-functional requirements](https://en.wikipedia.org/wiki/Non-functional_requirement) like testability, accessibility, reliability, etc, (often called “ilities” because of their common suffix) you probably haven’t seen “rewritability”, but I really want to add it to the pile.

I’ve often found in software engineering that counterintuitively, if something is difficult or scary there’s a lot to be gained by doing it more often. I think we can probably agree that software rewrites are [amoung](http://www.joelonsoftware.com/articles/fog0000000069.html) [those](http://www.neilgunton.com/doc/?o=1&doc_id=8583) [difficult](http://chadfowler.com/blog/2006/12/27/the-big-rewrite/) [and](http://onstartups.com/tabid/3339/bid/2596/Why-You-Should-Almost-Never-Rewrite-Your-Software.aspx) [scary](http://en.wikipedia.org/wiki/Second-system_effect) [tasks](http://steveblank.com/2011/01/25/startup-suicide-%E2%80%93-rewriting-the-code/).

Now that we’re starting to get better at service-oriented architecture, where networked applications are better divided into disparate services that individually have narrow responsibilities, a natural side effect is that it’s getting easier to write services that are replaceable later.

So what makes a piece of software rewritable?

**Clearly defined requirements:** not just what it needs to do, but also what it won’t do, so that feature-creep creeps into another more appropriate service. This one ends up requiring some discipline when the best place and the easiest place for a given responsibility don’t end up being the same service, but it’s almost always worth it.

**Clearly defined interface:** If you want to be able to just drop a new replacement in place of a previous one, it’s got to support all the integration points of the previous one. When interfaces are large and complicated this gets a lot harder and a lot riskier. In my opinion, this makes a lot of applications with GUIs very difficult to rewrite from scratch without anyone noticing (Maybe it’s because UX is hard. Maybe that’s because I’m terrible at GUIs.).

**Small:** Even with clearly defined requirements and interface, a rewrite is still going to be expensive and hard to estimate if there’s a lot to rewrite.

Any software engineers that have found themselves locked into a monolithic ball of mud application can see the obvious upsides of having a viable escape route though.

And once we’re not scared of rewrites, what new possibilities emerge?  Real experimentation?  Throw-away prototypes that we actually get to throw away?

How much easier is it to reason about a piece of software when it also meets all the criteria that make it easy to rewrite?
