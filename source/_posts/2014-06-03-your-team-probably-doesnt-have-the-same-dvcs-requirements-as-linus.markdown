---
layout: post
title: "Your Team Probably Doesn't have the Same DVCS Requirements as Linus"
date: 2012-01-03 07:43:58 -0700
comments: true
categories: 
---

Version control branches come with costs. I’m at the point now that I don’t think it’s possible to get away without spending a couple of days every month managing issues with version control and merging if you’re using feature branches liberally as is common with DVCS (like git) users. I’ve spent days myself in the past months, so I felt compelled to write this because those were days I could’ve been actually doing something that adds value instead.

The purpose of branching is to delay integration of some code into the main code line (for various reasons). There’s a heavy cost that comes from this in that the less often you merge, the harder it is to merge. I’m blown away by the effectiveness of automatic conflict resolution in git, but the bottom line is that if two developers are working in the same area of the codebase, [semantic conflicts](http://martinfowler.com/bliki/SemanticConflict.html) will emerge that need the intervention of a human to resolve. These can be complicated and tedious and involve multiple developers. Yes, branching is easier with DVCS, but this actually exacerbates a fundamental merging problem that DVCS doesn’t solve.

#“What if I keep my branches short-lived?”
There are some [better defenses for branching](http://dev-spout.blogspot.com/2011/07/feature-branches-are-not-evil-in-fact.html), like “What if I keep my branches very short-lived?”, and while it does mitigate most of the problems with merging, it also mitigates any advantage you think you might get from branching. If you’re only going to branch for a day, what’s the point?

#“Then how can I pick and choose what gets added/released?”
Merging early and often leads to simpler merges, but what about the case when you get partway through a feature and want to scrap it because you’ve come up with a better way? There are a number of ways to mitigate this problem, but if your need to “unmerge” occurs more often than your need to merge, you’ve probably got larger organizational issues to deal with. If those issues are purely technical, try more prototyping to uncover those issues earlier, and [feature-toggles](http://www.rallydev.com/engblog/2011/12/20/feature-toggles-branching-in-code/) for better control over what gets released. If those organizational issues are non-technical, like frequent changing requirements mid-feature-development then you simply need to get better (and probably smaller) [user stories](http://www.agilemodeling.com/artifacts/userStory.htm#Introduction) before commencing.

#“What if I do daily merges from the mainline into my feature branch?”
You’d think it shouldn’t matter which way you merge if you merge often, but that’s only fine if you’re the only one branching. As soon as someone else on the team comes along and starts up their own feature branch and follows your same best practice, the two of you are diverging from each other and creating merge-debt.

#Using a continuous integration server is NOT sufficient for actually practicing continuous integration.
I’ve heard of some teams using a bot to auto-add all branches to the team’s CI server, making sure that each branch gets put through the proper rigor of the CI server. This is actually cargo-cult continuous integration though because those teams are not actually continually integrating at all. Merging early and often is a prerequisite of continuous integration, by definition. Instead, running multiple branches in CI supports maintaining those multiple distinct branches for even longer, so you’re actually using the CI server to undermine the ideals of CI.  Even if you run a special build that tries to auto-merge all branches (yeah right!), but is not the mainline and is not intended for release, you lose the ability to regularly deliver work to some staging environment for manual regression testing.

#A small non-distributed team doesn’t have the same problems as Linus
If your team is in the same room and practices [collective code ownership](http://c2.com/cgi/wiki?CollectiveCodeOwnership) (instead of having a central maintainer) you should just do in-person peer code reviews (or better yet, pair programming) instead of relying on pull requests. It’s wasteful to force every aspect of intra-team communication to go through the computers in the room. I would even go so far as to say that if you’re in the same room, you don’t actually need a DVCS.

Most of the reasons behind feature branches seem to be a cure that’s worse than the disease itself. It’s vastly simpler for us to commit to the mainline at all times, early and often, and deal with deactivating or removing particular pieces of code in other ways (like feature-toggles) as those problems arise (which does not in my experience tend to be very often compared to how often I am merging new stuff in that stays in).

I don’t mean to be negative about DVCS either. I actually use git exclusively now, I think github has been a huge boon to open source, and I love anything that makes Linus more effective at maintaining my favourite OS kernel. It just really seems like feature-branches have never solved any real problem that I have, while they have caused a lot of pain.
