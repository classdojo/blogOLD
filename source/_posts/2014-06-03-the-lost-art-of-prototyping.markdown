---
layout: post
title: "The Lost Art of Prototyping"
date: 2009-12-26 17:19:01 -0700
comments: true
categories: 
---


Prototyping is a **design** methodology that basically involves “trying stuff out and seeing what works”. It’s meant to be iterative in that you continue to create prototypes (possibly by alterring previous prototypes) until you’ve got all the information you need to say your design is complete.

If we were building cars, we would probably first prototype a body design with CGI to be able to collect feedback before building the car itself. It’s much cheaper (effort and materials wise) to iteratively develop the body with a 3d model than with the actual materials that would be used.

If we were designing websites, we might prototype the design in photoshop for a bunch of iterations until the client is happy. The great thing about that is that the web designer can actually chop up that protoype in photoshop, and use it for images as part of the work after the client has approved the design stage. In this case, the prototype isn’t a throw-away prototype — it’s actually useful to bring into the implementation stage.

In software development we can (and usually do) prototype similarly. There’s usually a point in the design process where a developer needs to “try some stuff out and see what works”. Once the developer has proven a methodology with code, the prototyping phase can mostly be called complete. Throwing away that code would widely be considered a huge waste though, so it usually ends up being used in the final implementation as well.

# Prototyping VS. Hacking
It’s probably safe to say that many developers do prototyping (a design methodology) and implementation **at the same** time bouncing back and forth between the two as necessary, blurring that line between design and implementation.

This way of developing is seductive, because you get straight to banging on the keyboard, which feels like you’re making progress, but it’s really upstream in the design stage where you get the opportunity to save the most amount of time. If you don’t distinguish between design and implementation, it’s tough to tell which stage you’re in at any given time, and so it’s tough to determine if you’re in **the right stage**.

You can imagine how wasteful this back-and-forth would be if you were an automative engineer instead, and you swapped back and forth between prototyping and working on the implementation details. As you iterate on the prototype, those details you worked on in the last iteration could be completely removed — that’s a big waste of time, and it’s often emotionally difficult to let go of design decisions that have undergone a lot of implementation work. So while realistically design never really stops, you do want to do as much up front as possible.

So there are definitely right and wrong ways to prototype, but it’s extremely valuable and worthwhile if done correctly. I doubt many developers would argue that sometimes you just need to try stuff out and see what works. Very few developers are interested in development methodologies that omit the ability to prototype.

# So What about TDD?
This seems to me to be the most often used argument against Test Driven Development (TDD). I agree that TDD doesn’t work well for tasks that don’t have clear-cut solutions, but TDD is still always applicable downstream after the solution has become more clear. The trick is to reach a certain level of solidity with your solution’s plan *before* you get into TDD.

Here’s a case in point as [Ron Jeffries attempts to “solve sudoku” with TDD without even knowing the rules of the game](http://xprogramming.com/xpmag/oksudoku/). If you follow his method of solving the problem and compare it against [Peter Norvig’s design-first approach](http://norvig.com/sudoku.html), TDD starts to look like a miserable failure. Indeed, some have dragged this out as a case against the utility of TDD “in the real world”.  Ron Jeffries’ example doesn’t really make the case against TDD at all though; It simply shows that you have no business being in the TDD stage before you fully understand the problem and you’ve done adequate design. TDD doesn’t preclude other design methods (like prototyping) at all.

And in cases of large architectural issues, prototyping is likely not the first tool that you should turn to — it’s too detail oriented, and you can iterate much faster on designs expressed via whiteboard doodling, flowcharts, UML, etc. You might move to prototyping at some stage later though before you completely decide on some particular design. The important part to keep in mind though is that you’re **not** in the implementation stage — you’re planning.  Changes are cheap and easy at this stage, and it saves you so much more time than if you just jumped in and started developing.

The software that comes out of the prototyping process is a nice side effect, but it’s almost never ready for production. This is where TDD comes in. If you have a clear understanding of the solution you want to implement (whether you used prototyping or not) then your design is sufficiently complete to **start** TDD. In this way TDD and prototyping are not opposed at all. Prototyping is just one possible methodology in the design stage that should precede implementation. TDD just says that tests should be written before implementation. It doesn’t say anything about what else you do prior to implementation.

So, there’s nothing un-TDD about prototyping a solution, setting it aside, writing your tests, then writing an implementation that passes those tests (based on the knowledge you got from your prototype). Ideally you’re working with units that are single-minded and small so copying/pasting from the prototype isn’t even necessary, but to be honest, I think some copy/paste from the prototype is fine. If it’s done in a careful way where you’re not hurting the quality of the final code (because prototypes generally don’t care all that much about code quality), you might as well make use of your previous work, if you can. You just have to be careful that it’s the quality you want, but then again TDD will force a lot of the quality.

# The Steel Thread
The concept of [the steel thread](http://en.wikipedia.org/wiki/Steel_thread) is one that I use quite often on the team that I work in when we’re working on complex tasks. It’s definitely a loose sort of prototype, and it’s meant to prove the basics of our core concepts. Basically, we concentrate on the core functionality of the complex task, putting priority on the completion of the “[happy path](http://en.wikipedia.org/wiki/Happy_path)“, the path of execution without error scenarios, special cases, etc. Once that core functionality is in place, the general design can be considered verified, the necessary components can be easily identified, and the existing work can be evolved to something high-quality (possibly through a fresh start with TDD). Work is easily divided amoung teammates after this steal thread has been acheived.

# Spike Solutions
[Spike Solutions](http://www.extremeprogramming.org/rules/spike.html) are like the opposite of the steel thread in many ways. Where the steal thread tries to prove the viability of the entire solution (in a breadth-first sort-of-way), a spike solution will try to prove the viability of a part of the solution that isn’t very well known, in a depth first sort-of-way. It’s useful when there’s a particular piece of the solution that we’re not sure will work, so we prototype that part as quickly as possible to make sure our overall solution won’t fail because of that single part.

The point of the concepts of steel threads and spikes is to tackle the unknowns early on and prove the viability of the entire solution as early as possible. Once everyone is relatively sure that the team is on the right path and the design is firmed up, you’re ready to get into the more detail-oriented aspects of development.   It’s not until this point that I’d switch to TDD, and start writing my tests for the implementation stage of the work.

# Is this just [BDUF](http://c2.com/xp/BigDesignUpFront.html)?
I don’t think so.   I’m not proposing a huge documentation process that specifies every aspect of the final product.  I’m simply talking about spending some time to loosely figure out what we’re going to do before we do it.    It’s time well spent, because it’s just so much cheaper to make major changes at this earlier stage in the process.  We’ll still figure out the minor details as we go.
