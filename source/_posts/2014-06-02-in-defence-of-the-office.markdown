---
layout: post
title: "In Defence Of The Office"
date: 2014-01-11 15:51:15 -0700
comments: true
categories: 
---

I've been reading the 37 signals book [Remote](http://37signals.com/remote/) lately and it's got me thinking a lot about the advantages and disadvantages of working remotely.  While they clearly acknowledge that there are trade-offs to working remotely, I personally don't think they paint a very clear picture of just how expensive those trade-offs are.  I can only really speak from a software development perspective, but I think this might apply to other types of businesses where a high degree of collaboration is necessary and the concept of "team" is more than just "a group of people".

After 7 or 8 years of being a home-based contract-worker, and close to the same time spent working in various office environments, I've found that with the right people and the right environment, the office can be a lot more productive (and actually enjoyable) than a home environment, for a number of reasons.

Skype / Google Hangouts / Webex pale in comparison to actually being in the same room as someone else.  I can't explain why, because it seems to me like it should be good enough (and I really wish it were sometimes), but the fact of the matter is that it's not.  You miss nuances in communication that can add up to big differences in productivity.   I've been in hours and hours of pair programming sessions over webex: it doesn't match the high-bandwidth of shoulder-to-shoulder pairing.  I've done the shared whiteboard thing: it doesn't match the speed and simplicity of an actual whiteboard.

With communication over today's technological mediums, there's just a natural tendency to end the interaction as soon as possible "and get back to work" too, where people don't actually leave Skype / Google hangouts / webex running all day long.  The result is that people are reluctant to start new conversations like that because they're worried about interrupting the other person.  So people naturally fall back on less intrusive means of communication (text chat) and often even further back to more asynchronous forms of communication (email).

And asynchronous communication is not the boon to productivity that people think it is.  Email is today's definitive means of asynchronous communication, but I think it's pretty obvious that there are few methods of communication that are less efficient.  Imagine a sports team that can only communicate by email.  That would be ridiculous.  Email is amazing at its ability to cut down on interruptions of course, but it's at the obvious cost of timeliness and immediacy (not to mention the very real human aspects including general tone and emotional nuances!).

The ideal solution would be to solve the problem of interruptions without losing timeliness.

Explaining this really requires actually defining an "interruption":  When you're on a team and someone wants to talk to you about the main goal of the team, that's decidedly NOT an interruption.  Imagine a quarterback being annoyed by the "interruption" of someone yelling that they're open for a pass.  Imagine a soldier in a firefight being annoyed at another soldier for requesting cover fire prior to some forward manoeuvring.  In order for something to really be an interruption, you have to be working on a different priority than the other person, one that you think is of higher priority.

In a collaborative environment, interruptions should often be viewed as a symptom, and not the actual cause, of the problem.  To solve the problem of interruptions at the root, you've got to clearly define the priorities of the team, aligning everyone on those, and concentrating as many people as possible on the top goal rather than going the easy route (management-wise) and doing something like giving each of the X members of the team one of the top X priorities, effectively "[team-multi-tasking](http://brodzinski.com/2013/11/multitasking-teams.html)".  Team-multi-tasking is a common approach because:

* It's the easiest thing to do management-wise (Why bother prioritizing when I can have X tasks worked on at once?).

* It feels like you're getting more done, because so many things are in progress at once.

* It ensures everyone is 100% utilized.

But it's also pretty obviously the absolute slowest way to get your top priority shipped and to start getting value from it  (and often [the slowest way to get them all done](http://www.startuplessonslearned.com/2011/09/power-of-small-batches.html), believe it or not!).

Not only that, but the more you do this, the more people tend to specialize into roles like "the back-end guy" or the "[ops guy](http://en.wikipedia.org/wiki/DevOps)", etc, and individuals lose the ability to be cross-functional, and to practice [collective code ownership](http://www.extremeprogramming.org/rules/collective.html).  It's a vicious cycle too: the more an individual tends toward deep specialization, the more we're tempted to give them that kind of work because they're the best at it.    Not only does your [bus factor](http://en.wikipedia.org/wiki/Bus_factor) skyrocket, but you get back into these scenarios where anytime someone engages someone else for help, it's an interruption to that other person, so people tend to not ask for help when they really should, or they use dog-slow asynchronous methods (like email).  Breaking this cycle means constantly trying to break down these specialty silos for any given specialty by having more experienced people collaborate with (and often mentor) less experienced people.  The end result is a team that *makes* full-stack engineers and not just one that hires them.

I find that the right mindset for the team is to create an environment that would be best for a team working on only 1 super-important thing that you want to start getting value from as soon as possible.  A general rule of thumb is:  If you're having a text conversation with someone in the same room, you're doing it wrong.  I know that's common, but if you think about it, it's pretty absurd.

**How would that environment look?**  It would be a "[warroom](http://www.sciencedaily.com/releases/2000/12/001206144705.htm)" for [radically collocating](http://www.ibimapublishing.com/journals/CIBIMA/2010/959194/959194.pdf) the team.  Everyone that needs to be there would be there, arranged in a manner that's most effective for verbal communication.  There would be nearby whiteboards for collaborative design sessions, and [information radiators](http://alistair.cockburn.us/Information+radiator) to show the progress of the efforts and various other metrics of the current state of affairs by just glancing up.

**How would the team behave?**  They would be a "tiger team".  They would all be helping to get that one thing out the door.  They would almost never use any electronic means to communicate (except obviously, when it's more efficient, like sharing chunks of code, or urls), and you'd never hear someone say "that's not my job".  If someone is the only person that knows how to do something, the team identifies them as a process choke-point and quickly tries to get others up to speed on that skill or responsibility (and not by giving them links to docs or occasional hints, but by super-effective methods like [pair programming](http://www.extremeprogramming.org/rules/pair.html), in-person demonstration, and actual verbal discussion).  If one member of the team appears to be stuck, he asks for help, and if he doesn't, the other members notice, and jump in to help, unprompted.  There are no heroes, and everyone takes responsibility for everything that the team is tasked with.  This can and should be taken to extremes too:  members should drop their egos and make themselves available to do grunt work or testing for other members -- whatever gets the top priority shipped as soon as reasonably (and sustainably) possible.  This includes making yourself vulnerable enough to ask for help from others, not only for tricky aspects of your work, but also just to divide your work up better.  If you're taking longer than expected on a given task, you should be conscious enough of that to be openly discussing it with the team, including possible solutions, and not trying to be a hero or a martyr.  Conversely, you should never be waiting for extended periods of time for your teammate to do some work that you depend on for something else.  If a teammate is taking longer than usual, jump in and help.

**How would management work then?**  The team should self-organize.  With clear priorities set, the team can and should, for the most part, self-direct.  A manager should not try to manage the avalanche of interactions that happen during free-collaboration throughout the day.  Trying to manage who works on what, will simply make that manager a choke-point and slow the process down (and he/she will inevitably be wrong more than right, compared to the wisdom of the entire team).  Often a non-technical manager can have the advantage over more technical managers, because he's forced to trust the team's decisions and doesn't become an "approval choke-point" for the team's engineering decisions.

That doesn't mean a management role is unnecessary though; it's actually quite demanding to manage a team like this.  Priorities must always be crystal clear and for the most part, the top few priorities being worked on should not change very often.  If they do change often, you usually have either a management problem or a product quality problem.  Those problems should be fixed at the root as well, rather than making developers feel like management or customers are just a constant stream of interruptions.  Keep in mind that if you do change the top priority often enough, you can completely prevent the team from any progress at all (I've spent months on a team like that before -- it's not fun for anyone).  (For a more complete description of the ideal responsibilities for this style of management, see "The Management" [here](/blog/2013/05/07/a-requiem-for-a-team/) )

Does this work for all types of people?  No.  But then again, you'll never get a fast team of developers without hiring the right people.  If you have people on the team that are incapable of being team-players, it's certainly not going to work (and you'll likely have a number of problems).

**What if we have TWO top priorities though?**  Flip a coin and pick one; It's that simple.  Just arbitrarily choosing one will get one of them shipped and returning value as soon as possible.

**What about team member X that has nothing to do?**  The team should recognize this and:

* try to break down the tasks better so they can help (it's often worth a 30 minute session to bring other people on board -- Any given task can almost always be broken down further with additional design discussion, even if its not worth dividing up the work).

* try to get them pair-programming so they can learn to help better.

* try to get them testing the parts that are done.

Obviously in some scenarios it might make sense for them to start on the second priority, but they should be ready to drop that work at any time to help get priority #1 out the door faster.  **Remember:** the goal is to ship finished features faster.  It's not to keep the people on the team as busy as possible.

**Isn't that really tough on the developers to rarely have quiet time to concentrate?**  Yes, at first it often is, often because focusing on the top priority requires discipline because it's different from the status quo.  And people simply aren't used to the buzz in the room.  The longer you spend working with headphones on, trying to carve out your own niche, separate from the rest of the team, the longer it will take you to transition and the harder that transition will be.  But soon you learn to ignore the irrelevant buzz in the room and to tune back in quickly when it's important and relevant.  And since you're all working on the same thing, it's often relevant, and lot less difficult to get back into the [flow state](http://psygrammer.com/2011/02/10/the-flow-programming-in-ecstasy/) than you'd expect (especially if pair programming).  So the pay-off for developers is:

* huge productivity improvements

* less waiting for someone else to do their part

* longer sessions in "flow state" and easier returns to flow state

* less solitude without adding interruptions

* less "all the weight is on my shoulders" scenarios

* more knowledge sharing and personal development

It helps a lot if developers take breaks more often, because you actually end up spending a lot more time in the flow state in a given day.  You end up learning more from other developers and being vastly more productive as well, which is exhausting and energizing at the same time.  In my opinion, when done right, it's just a lot more fun than isolated development.

Of course it often also helps to have break-out rooms for smaller prolonged conversation when desired as well.

**But what if you have dozens of engineers?**  It's just not reasonable to try to make teams that contain dozens of engineers.  [Brooks' law](http://en.wikipedia.org/wiki/Brooks%27s_law) has seemed to hold fairly well over time and he explains that one reason is that the more people you add to a group, the more communication overhead there is.  I've personally seen this as well, with team-size starting to get diminishing returns between  8 and 12 people, with little value (if any) to adding members beyond that.  When you get beyond 8 people on a given team, you need to start thinking about creating a second team.  [Conway's Law](http://en.wikipedia.org/wiki/Conway%27s_law) seems to dictate that a [service-oriented architecture](http://en.wikipedia.org/wiki/Service-oriented_architecture) is the best solution we're going to get for scaling up an organization's developer head-count, but I've personally found that smaller codebases with distinct responsibilities are generally better codebases anyway.

With all that said, of course I really wish I could work remotely sometimes and get all the same benefits.  I've simply never seen a telepresence technology set-up that matches the fidelity of actual face-to-face and shoulder-to-shoulder collaboration.  Maybe it exists.  I'd love to hear about it.  But my experience simply doesn't indicate that the current status quo technologies (skype, webex, etc), like Remote recommends, are up to snuff.  The way it stands today, I'll almost always put my money on a collocated group of ["team-players"](http://avichal.wordpress.com/2011/12/16/focus-on-building-10x-teams-not-on-hiring-10x-developers/) over a geographically disparate team of "gurus".

