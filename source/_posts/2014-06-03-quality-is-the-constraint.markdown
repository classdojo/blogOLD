---
layout: post
title: "Quality is the Constraint"
date: 2010-12-05 15:33:50 -0700
comments: true
categories: 
---


One fine day in the trenches, a junior engineer was tasked with optimizing a particular web service call that was way too slow (sometimes slower than 20 seconds!).  I had just figured out how to use a performance profiler for that particular platform, so I thought I’d offer to show him how to use it.  His response was that he was on a tight deadline and didn’t have time to learn to use the profiler, and that he was just going to tune the database calls to make them perform better.

Later in the year when the problem still wasn’t solved, I had a chance to take it on myself.  The profiler showed me that this service call was itself making around 20 web service calls to a second system that could obviously add up to 20 seconds, if that other web service took 1 second for each of its responses (and the logs showed that sometimes it did).  It turned out that almost all of those web service calls were redundant and completely unnecessary.  Simply removing them (which took about 1 day of effort) shaved 19 seconds off this web service call’s duration in production in some cases.

The total execution time spent on database calls was 5 milliseconds.  A 50% improvement there would probably take a week’s worth of effort, and really only get you 2 or 3 milliseconds of performance improvement.

The moral of the story is that there’s a pretty simple process for optimizing a system:

* Identify and isolate the component that is tying up the most time in the system  (let’s call it the bottleneck)
* Optimize that component to make it less wasteful
* Repeat

Skipping step 1 isn’t a shortcut.  It’s absolutely critical to know that you’re optimizing the bottleneck, and not some other random component.

This is pretty obvious stuff for most experienced developers of course.  And while they seem to know to apply this to the systems that they work on, it’s more rare that they notice it outside of the code and see it in the process of software engineering in general.

The software development *process* is a system as well, made up of components.  Requirements come in at one end, and deliverables go out the other end.  As people who are involved in that process, we naturally want it to be more and more efficient.  We are constantly trying to figure out how to optimize that system so we can deliver better software in less time.

So step 1:  Identify and isolate the component that is tying up the most time in the system.

Not every team develops software the same way, so this component of the process could be different team by team.  In practice though, I’ve always seen teams spending the most time doing these sorts of things:

* Refactoring poorly written code so that features can be added
* Learning/relearning existing code that has long since swapped out of all developers’ “mind pages” (for extension or bug-squashing).
* Debugging
* Performing Manual User Acceptance Testing (by both developers and testers)
* issue tracking (administration of that tool and issue in it)
* discovery and documentation of steps to reproduce
* triage (what bugs to squash first?)
* communication between customers, support, QA and developers
* customer support
* customer dissatisfaction leading to churn and reputation problems (affecting the entire organization)

All of these time consumers are affected directly or indirectly by our ability to control quality.  In my experience, the majority of the software development process isn’t hung up in requirements analyis, design, or implementation.  It’s hung up in all these Quality Control related issues.  Quality Control is the constraint that keeps us from creating the right software faster.  Steve McConnell confirms it in a more scientific way than I ever could:

> The rest of us would do well to learn from a discovery made by IBM in the 1970s: Products with the lowest defect counts also have the shortest schedules (Jones 1991). Many organizations currently develop software with defect levels that give them longer schedules than necessary. After surveying about 4000 software projects, Capers Jones reported that poor quality was one of the most common reasons for schedule overruns (1994). He also reported that poor quality is implicated in close to half of all canceled projects. A Software Engineering Institute survey found that more than 60 percent of organizations assessed suffered from inadequate quality assurance (Kitson and Masters 1993). On the curve in Figure 1, those organizations are to the left of the 95-percent-removal line.

([http://www.stevemcconnell.com/articles/art04.htm](http://www.stevemcconnell.com/articles/art04.htm) — The whole article is extremely illuminating)

What this means is that if we really want to move quickly, we need to take a good hard look at how we manage quality.  Of course this is counter-intuitive, and its actually hard to swallow, because ensuring quality can be mundane and tedious if you’re not doing it right.  But as developers we’d be silly to ignore the real bottleneck in the process, and optimizing for that.  Micro-optimizations elsewhere in the process will yield very little benefit compared to improving measures that ensure quality.

As developers, we love to argue about and discuss these micro-optimizations all day long:

* [what text editor you use](http://en.wikipedia.org/wiki/Editor_war)
* [how important input speed is](http://steve-yegge.blogspot.com/2008/09/programmings-dirtiest-little-secret.html)
* [IDEs vs. editors](http://stackoverflow.com/questions/136056/ide-or-text-editor)

It sure seems silly though to be pursuing micro-optimizations, at the expense of tackling the real #1 time-suck:  Quality.

