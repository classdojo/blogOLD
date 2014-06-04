---
layout: post
title: "Agile: The Good Parts"
date: 2011-09-14 07:51:37 -0700
comments: true
categories: 
---

Let’s just forget about story points, pigs, chickens, daily stand-ups, burndown charts, sprints and scrummasters for a second.  In my experience all of that weird jargon is really hurting Agile’s adoption among the no-nonsense type of developer that doesn’t have time for fluff and wants to know the real benefits of something before investing time in learning about it (instead of a million other things they could be learning).

I’ve also seen that when anyone happens to cite a failed experience with Agile, the explanation from Agilists is invariably the cryptic “you weren’t doing it right”. This is a bit of an irritating response to anyone that’s spent a significant amount of time following the ceremonies and speaking the lingo though.  Instead I’d like to submit that you have a much better chance of succeeding with Agile if you know the real reasons behind the madness.

There are a number of Agile values I’ve noticed in my years of practicing scrum and XP that I think stand on their own even if you’re not doing Agile and just want to improve your development process in some small way.  I’m going to list them (and try to stay jargon-free) because I imagine that they would be useful individually, but they do have a sort of self-reinforcing quality to them where their effects will somehow be amplified if you use them together.  You should also feel free to break the rules where you feel they need to be broken, but I’ve very rarely found that to be necessary.  Usually when I’ve broken these rules, I’ve regretted it later, because what I thought was an exception didn’t really end up being an exception.

# Create a team, not just a group of individuals.
A project will move faster when it is being developed by a team that self-organizes around its goals rather than a group of individuals working separately.  Here are few rules of thumb to creating a team instead of just having a group of individuals:

* Don’t assign tasks to individuals.  Let the team figure out who works on what, and let the team take responsibility for all tasks rather than individuals.   Everyone on the team needs to agree on what it means to be done and how, and everyone on the team needs to take responsibility for it.
* Strive for cross-functional skillsets.   Let the team members teach each other so they can better help each other in the future rather than allowing one person to become the bottleneck for any particular kind of task.
* Try not to change team size or membership very much.  A good team can be a fragile thing.
* Throw out the notion of individual code ownership. The entire team owns the code.
* Create more of a bullpen environment where the team members are all basically in the line of sight of one another and can just talk to one another about what they’re working on.  This was tough, because it made us give up our individual offices, telecommuting, and deciding our own hours, but it was well worth it for the improvement to the quality of our work day.  Almost anytime a developer has to use some means of communication other than his voice to talk with a teammate, you have unnecessarily wasted time.
* Put QA personnel on the team so that testing can be can be on-going and so the team can more easily take on QA and testing as a team-wide responsibility.
* The whole team needs to agree on what kind of work is necessary for each task before it is to be considered “done”.  (coding standards, documentation standards, how rigorously they test, etc, etc)
* The result of this was a highly capable team that could “swarm” to complete goals reliably and quickly.  We actually developed a sort of sports team mentality that made this way of working genuinely fun, and helped us push ourselves to be better all the time.  There are a lot of challenges to creating a great team that can inter-communicate openly and honestly, but it’s an amazing thing to behold when it happens.

# Estimates need to come from developers.
This is can be very hard for some organizations to swallow, but developers are the ones that are most qualified to do estimations, and as professionals, they should be working diligently to improve their estimation capability.  When a developer is responsible for estimation, that developer feels a sense of ownership about his work and will feel a vastly greater sense of responsibility to meet the estimate.  Developers that have never learned how to estimate will not be good at it at first, but there’s no other way for them to get good at it than to have them do it.  There are a few major things that can vastly help estimation too:

* Always break work down into tiny chunks.  We generally broke work up into chunks that were less than 3 days of effort.  I’ve never seen a task that couldn’t be broken down into subtasks that are this small or smaller, if the developers are so inclined.
* The team should take a look at bad estimates in retrospect and figure out where they went wrong.
Recognize work that will be impossible to do due to lack of clarity from the business, or unmet dependencies and push to have those requirements met.
* For highly speculative work, just commit to doing a proof-of-concept, or time-boxed research.
* The more developers that are involved in the estimation process, the better.  You’ll probably want to include QA/testers as well, because good ones have unique insights.

# Context-switching should be avoided *mercilessly*.
This means that each developer needs the discipline to make sure he only works on one task at a time, that the team works on as few tasks at one time, and that developers need sustained uninterruptable timeboxes where the priority of work is not allowed to change.

Most people (especially non-developers) have no idea how much of a huge time-suck that context switching is, and few realize how seldom it’s actually worthwhile.  Also if the team is tackling as few tasks as possible at once, if any task can be finished by having more developers on it at once, then that’s what the team should do rather than starting as many tasks as possible and working on them in parallel.  This might sound counter intuitive, but with the team ultra-focussed on as few tasks as possible at once, they can get the totality completed faster.

# Try to always improve.
The team must commit to continually improving. At regular intervals, the team should look at how things are going and pick a few actionable things to make their work better/faster/easier.  You’d be surprised at the huge speed improvements that can come from this practice over time.  If the team has a shared calendar, set up a reoccurring meeting at a regular interval to have this meeting, and be laser-focussed on deciding what improvement you want to achieve and how exactly you’ll try to achieve that.  We’ve always set aside 1 hour per week, but your mileage may vary.  Start every meeting by evaluating how successful the team was with the previous meeting’s goals.

# If something is difficult or time-consuming, do it more often.
This sounds crazy to the uninitiated but there are two reasons for this:

1. Doing difficult things more often will drive out new creativity in making them less difficult.  Pro-tip: Automation is almost always the answer when the problem is testing (See [TDD](http://www.agiledata.org/essays/tdd.html), [BDD](http://en.wikipedia.org/wiki/Behavior_Driven_Development), [ATDD](http://testobsessed.com/2008/12/08/acceptance-test-driven-development-atdd-an-overview/)) or deployment.  (See [Continuous Delivery](http://continuousdelivery.com/))
2. Many types of tasks get more difficult the longer they are postponed and so are always easier if you do them more often instead of letting the risk of complexity pile up.  Integrating code into the main branch is one example  (See [Continuous Integration](http://martinfowler.com/articles/continuousIntegration.html)).  Deploying is another (See [Continuous Delivery](http://continuousdelivery.com/)).

# Be merciless about achieving high quality
Over the long haul, [speed comes from quality](/blog/2010/12/05/quality-is-the-constraint/), so everyone on the team needs to make quality their job.  Everyone needs to test, and everyone needs to think about how to continually make testing easier without cutting corners.

* Have QA personnel on every team, and have them testing as the team works.
* The whole team needs to agree on what level of quality is needed, and what quality metrics will be used to judge every check-in.
* Perform a root-cause-analysis on each defect.  Try to figure out how to avoid that class of defect in the future.

#Do everything in tiny increments.
Tiny increments reduce the risk of compounding problems, and allow you to get feedback and correct your course more often.

* break-down your work into tiny tasks
* plan just-in-time and just enough to do work.
* test as you go, instead of in huge batches
* merge code to the mainline early and often.
* deploy early and often.
* don’t add anything to the system that you don’t need until you need it ([YAGNI](http://c2.com/xp/YouArentGonnaNeedIt.html))

# Get customer feedback early and often
Get customer feedback early and often to converge on the best possible solution as fast as possible by constantly correcting course instead of blindly following some long-running plan or doing unnecessary work.  The customer’s priorities and vision of the product will change as he sees results, so it’s better to not find out about these changes after a lot of unnecessary work has been done.

* Do work in priority order as dictated by the customer.  This will allow them to see the aspects that they care about most as early as possible, and therefore help you converge on a unified vision of the product faster.
* Work break-down is better done in vertical slices where the customer can get some amount of real value from each piece (or at least see some evidence of work) rather than having many non-user-facing tasks, where possible.  This allows for more potential for feedback.
* The work shouldn’t be considered done by anyone on the team until the customer, or a representative of the customer agrees that it’s done.
* Constantly improve estimation skills so that they are generally more reliable so the customer knows the cost of the work he has requested and can make realistic decisions based on that.

Anyway, feel free to try what you want and throw out the rest!
