---
layout: post
title: "Release-ophobia"
date: 2013-03-16 07:33:09 -0700
comments: true
categories: 
---

If you’ve developed SaaS in a large organization (or even a small organization that acts like one), you’ve probably seen some of the symptoms of fear of releasing software:

* Off-hours deployments and weekend deployments
* Infrequent releases
* extended code-freeze and testing cycles
* Reluctance to refactor
* Feature branches for the purpose of ‘cherry-picking’
* release managers
* many non-customer-facing environments before production.

These symptoms usually happen only in larger/older organizations, because of two factors:

* They take a lot more personnel / time to implement than smaller organizations have.
* They are usually processes and attitudes that are collected as a reaction to problems that occur in the course of a company’s lifetime.

#“But you can’t be too careful!”
One problem is that you CAN indeed be too careful. It’s absolutely imperative that the costs be considered as well, if you want software development to still go reasonably fast. Otherwise these manual preventative processes will slowly creep in over time and your team will be releasing at a snail’s pace.

The other problem is that these policies alone are in some ways not careful *enough*. Where are the techniques for mitigating defects that inevitably still slip through? Where are the techniques to detect them, limit the customers exposed, and limit the time that customers are exposed?

All of these symptoms have a few things in common: They tend toward heavy **manual and preventative** process added generously over time, usually with little thought to the cost/benefit ratio of such process. It’s all too common for every production issue to result in a new process to prevent it, without regard to how infrequently that problem might occur, how damaging the result is, or how easily it is rectified.

# So how do we keep bugs from getting to our customers?!?
Non-preventative measures (I call them “**Reactive Measures**“) do indeed exist, and can help you safely maintain a fast and steady flow of new features to customers.

* [Feature-Flags](http://code.flickr.net/2009/12/02/flipping-out/) allow you to commit incomplete work to master and push it to production safely. Customer-specific feature flags allow you to test in production or enroll customers in a beta program. With a good feature-flag system, it’s even possible to release a feature to only a certain percentage of customers, and to watch your metrics to see the effects.
* **Easy/fast (read “Automated”) deployment.** If deployment takes a long time, then you can’t afford to deploy often. Also, if you can’t deploy quickly, you can’t redeploy quickly (in the event of a problem).
* **Easy-undo.** Rolling back from a defective release to a known-good release is the simplest and fastest way to recover from defects, if the process is both quick and easy. Defects will happen no matter how much prevention you use: Easy-undo can mean the difference between light customer impact and heavy customer impact.
* **Smaller releases.** Smaller releases have less code, and therefore generally less bugs. Because they don’t contain many changes, they’re easier to test and a rollback is less-likely to negatively impact a customer. Also when a production defect appears in the latest release you have much less code to sift through to determine the cause.
* **Practice Continuous Integration** ([which necessarily involves always committing to master, and only incidentally has to do with using a CI server](/blog/2012/01/03/your-team-probably-doesnt-have-the-same-dvcs-requirements-as-linus/)) . Feature branches, infrequent commits, and committing non-production-ready work are all practices that need to be avoided, because they are all time-consuming delaying mechanisms.
* **“Done” == “In Production”.** If the team moves on to new features before the last one is in production, then that last feature is obviously unnecessarily being held back from release. They will be faster if they deliver to production and ensure it functions there properly before moving on to new features because it avoids unnecessary and time-consuming multi-tasking. This goes hand-in-hand with smaller, more frequent releases.
* **Comprehensive Automated testing.** When you deploy more often, you need to test more often. The cheapest way to do this is with comprehensive automated tests. While they’re a heavy-upfront cost, if you run them as often as possible, they’ll pay for themselves very shortly.
* **Continuous Production testing.** Create automated *black-box* integration tests for some of your most important features and figure out a way to run them repeatedly and continuously against your production deployment so that you know instantly when those features are broken. There’s no need to wait for customer feedback to learn about a faulty release.
* **Searchable, aggregated logging with proper log-levels.** Making your logs easily searchable in one place makes them something that developers will actually use for defect detection and for debugging. They can go a long way to making your application more transparent.
* **Runtime monitoring, runtime metrics and information radiators (most importantly alerts).** Instrument the things you care about most, and have alerts sent out when the measurements are abnormal.

**Note:** Of course some preventative processes are necessary, but when they are, automation is almost always preferable to time-consuming manual human processes.  Either way, you should consider the cost of the process and determine if it the fall-out from the type of defect it prevents is actually worth that cost.

In the end, a fear of releasing is a fear of change, and a fear of change is a fear of improvement. This is a crucial lesson that Big Company software teams can learn from the small, scrappy start-ups that are quickly trying to disrupt them. The more often you release, the more often you can test hypotheses and get customer feedback, and the more often you can course-correct. Companies that don’t realize this are susceptible to being leap-frogged by competitors that do.
