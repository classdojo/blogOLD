---
layout: post
title: "The Future Proofing Trap"
date: 2009-12-20 17:27:28 -0700
comments: true
categories: 
---


> “We will encourage you to develop the three great virtues of a programmer: laziness, impatience, and hubris.” — [Larry Wall](http://en.wikipedia.org/wiki/Larry_Wall)

In this quote Larry Wall makes some great points about what it means to be a great programmer in a zen-like,  toungue-in-cheek sort-of-way.  Let’s look at one aspect of the Virtue of Laziness.

Every reasonable developer knows that he should write his code to be easily maintained.  As part of that work, it’s natural for that developer to want to try to make his code as ready for future change as possible.  Taking that desire a few steps further, he might want to write code that solves future needs in addition to the current requirements, so that that code doesn’t even need to be revisited.  Unfortunately, that’s a common mistake that leads to a lot of wasted time and **less** maintainable code.

I’d like to propose a principle of software development that I’ve come to believe:

**The most maintainable code is the simplest possible code that meets all the requirements.**

This is almost a tautology because simple code is (by definition) easier to understand, so it’s easier to change/enhance/extend.  Code that does more than what’s currently necessary is not as simple as it could be though, so it’s not as maintainable given the current requirements.

One might argue that code that does more than what’s necessary can meet future requirements without change, thereby proving itself to be more easily maintained (no maintenance required!), but all of that hinges upon the developer’s ability to consistently and accurately foresee future requirements.  Otherwise that developer has:

* wasted time developing unnecessary functionality
* decreased the maintainability of the codebase

# Even when everybody is pretty certain of the future requirements…
Now let’s consider the case where the developer is almost absolutely sure that the requirements will change a certain way, and so the code should be written to handle that scenario as well.  Wouldn’t it be better to do that work now?  No.  It still takes more time and effort (at a time when we know its not necessary), and it’s still less maintainable code until those requirements change (in case other unrelated changes are required).  On top of all that, there’s *still* risk that the requirements won’t change in the anticipated way!

# Even when everyone is absolutely 100% certain of the future requirements…
Now let’s consider the case where everyone is 100% certain that the requirements will change in a specific way, and you can write your code to handle that way as well as the current way.  In that infrequent scenario, you don’t face a bunch of losing propositions, so it does make a bit more sense.  However, I’d still like to pose a question:  how much more work is it to do the additional work later instead of now?  Truthfully, the amount of effort is virtually identical regardless of whether you do it now or later.  That means you can enjoy maintaining the simpler version until the time comes that it needs to be changed to meet new requirements.

This isn’t a new idea I’ve dreamt up: it’s the [YAGNI](ttp://c2.com/cgi/wiki?YouArentGonnaNeedIt) principle, and it’s an essential part of [Uncle Bob’s 3 Rules of TDD](http://butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd).  It’s also a great way to avoid unnecessarily complex code.

(It’s important to note too that YAGNI doesn’t say to avoid making your work as futureproof as possble.  YAGNI just says not to put extra code into making that possible.  For example, if you create a class for a UI button that will be used to save some user data in a form, don’t call it “UserDataSaveButton” — just call it “Button”.  It’s no extra work and the re-usability possibilities have increased dramatically.)

We’re not engineers building bridges;  we don’t work with unchangeable steel and concrete, and we can accomodate changing requirements easily.  It’s unrealistic and wasteful to guess that we know what future requirements will come, especially when the potential work saved in the long run is neglible.
