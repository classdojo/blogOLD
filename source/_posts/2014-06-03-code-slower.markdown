---
layout: post
title: "Code Slower"
date: 2014-06-03 17:32:30 -0700
comments: true
categories: 
---

Here’s a controversial opinion, but one that I really believe to be true: most of the things we do to produce code faster are actually counter-productive.  It sounds crazy, and I would naturally oppose it except that every time I ignore this lesson, experience has a way of reteaching me.  This is as much a message to myself as it is to anyone else that might happen upon it (I’m talking to you, viagra comment spammers).

# Development Time VS. Maintenance Time
There’s no doubt that the original development stage of a piece of software can be time-consuming.  It’s interesting though, when you consider the difference in time spent in development vs. time spent in maintenance.  At what point do you cross into maintenance mode?

Let’s face it: you’re actually also in maintenance mode pretty much right away, unless you’re some superhuman that conceives of the whole system at once and doesn’t make any design tweaks (or even typos) while coding.  But you’re not.  So the development-time VS. maintenance-time dichotomy is a false one.  You’re always in maintenance mode.

# Invest Early, Invest Often
So if you spend so much time (all your time) in maintenance mode, then it makes sense to do every little change and tweak in such a way that your subsequent tweaks and changes are as easy as possible.  We should be spending the majority of our energy optimizing our time spent on maintenance and not our time spent on development.

Now it’s natural that one might say “well why not optimize both?”, and that’s a valid question.  There’s no good reason not to try to optimize both, but we have to remember to never ever ever optimize the development process at the expense of the maintenance process, simply because we just spend **so** much time in maintenance mode.

# Some examples
## Skipping the planning stage.
This is generally caused by the “Weeks of coding can save days of planning” fallacy.  Uncover all the main parts of your design **before** you code yourself into a corner that requires a near-rewrite to escape.

## Writing untestable code or skipping unit-testing
Unit-tests are your insurance that future changes don’t cause non-obvious regressions.  They also have a magical way of creating better factored, higher-quality code.  If you skip this stage, your code **will not** be factored as well as it could be, and come maintenance time, you’ll be scared to make changes for fear of breaking something somewhere else.

## Writing classes and functions that do a lot
This one is a really seductive one.  We want to be **consumers** of classes and methods that do a lot for us, because higher levels of abstraction are how we get more done in less time.  From the consumer stand-point, this makes lots of sense, and it’s actually the best way to improve development speed and maintenance speed at the same time.  If you’re also the person writing the class or function that does more though, you have to be very careful to use the highest abstractions possible for that as well, even if you’re writing its inner abstractions as well.  What this means is that every level of abstraction does as little as possible, and you build up to the level of abstraction that you want with those thin, thin layers.  Classes and functions that try to do a lot instead of relying on other classes and functions are very hard to maintain, simply because there’s so much to do read and understand, and there’s no easy way for the maintainer to skim and decide what piece is relevant, because the pieces are doing multiple things.

## Leaving code in a low-quality state
I’m talking about everything involving non-readable and poorly factored code, including bad names, foggy separation of concerns, etc.  Code should not be written just for the machine.  It needs to be written for the next guy that comes along as well.  That next guy could be you.  Or a [violent psychopath](http://wtfcode.net/post/193202062/always-code-as-if-the-guy-who-ends-up-maintaining)

## Using code generation
Code generation is just pure evil, if there’s ever a remote chance a human will ever have to read it or change it.  A computer program doesn’t know how to write code that a human will understand, and human understanding is exactly what we need to strive for if we care about making maintainable code.

# Understatement of the day:  You’re more than just a typist
It’s largely irrelevant if you can touch type at 90 wpm.  It’s largely irrelevant if your IDE can do automated refactors.  It’s largely irrelevant if your efficiency with Emacs or vim makes you look like Neo in The Matrix.  These things are great bonuses, but won’t make much difference to your proficiency (and efficiency) as a programmer if you neglect to first consider the maintainability of your codebase.  (Corollary:  In the name of all that is good in this world, please don’t name your variables p1, atb, etc, or your functions like atoi() just for the sake of saving keystrokes!)

Time and time again my mistakes remind me:  there’s only one way to be more productive over the long haul: work with better, higher abstractions.
