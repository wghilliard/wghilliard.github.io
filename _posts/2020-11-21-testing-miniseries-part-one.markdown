---
layout: post
title: Opinion - Testing Miniseries - Part One - The (Formulated) Cost of Inadequate Testing
date: 2020-11-21
categories: opinion development
---

WIP Disclaimer - All content is subject to change!

---

I've decided to break down my initial attempt at discussing this topic of *The Cost of Inadequate Testing* in to a miniseries of articles - welcome to Part One.

---

Often I find that the value of testing is difficult to measure, however the cost of inadequate testing is quantifiable.

There are many projects out there, all with constraints and caveats that make test strategies arguably unique. One might claim that common layers of the stack can be addressed in common manner. For example modern HTTP web servers often include a testing framework, and special runtime environments like Android or iOS have frameworks that provide conventional patterns to setup the environment and make assertions.

However, something that often goes unconsidered is the cost of the tests written and the value they provide.

## Formulation and Terms

In this article I shall attempt to formulate the perceived cost to develop a **Product** over its entire lifecycle. Terms are in **bold**.

For this thought experiment, we'll express costs in the units of "developer hours", the trendier version of a "man hour".

When we build a **Product**, we can think of it as a composition of an environment (**Infrastructure**), some business logic (**Features**), and undetected bugs (**Defects**).

> Product = Infrastructure + Features + Defects

Caveat - **Infrastructure** is a topic for another day, for this exercise we can pretend that if the code builds in the Continuous Integration pipeline, then it performs (as authored) in the production environment.

Therefore, let's zoom in on the **Features**. Each **Feature** needs to be described, designed, built, and updated as the product evolves. Easy enough!

> Feature = Design + Implementation + Maintenance

Each of the above terms could be expanded further, but let's unpack the **Implementation** and **Maintenance** terms.

**Implementation** is best described as writing the code, bringing the design in to the world of the living.

**Maintenance** encapsulates both updating the business logic as the **Product** evolves, and addressing defects as they are found.

Lastly, let's assume the **Product** exists on a timeline, where any given point on the timeline can referred to as **T** (or **t**) where **Product(T)** is the cost of the **Product** at time **T**.

And we'll pretend we can deliver a new feature at each increment of **T**.

**E** is the sigma operation, so something like **E(T=0, Now) {Foo(T)}** describes the sum of **Foo** for every value of **T** between **0** and **Now**. For example:

> E(T=0, 4) {2 \* T} = 0 + 2 + 4 + 6 + 8 = 20

The left side term will be the _total_ cost of the Product, which each iteration of the formula expressed via the letters of the Greek Alphabet.

> \$Alpha = Product(Now) = E(T=0, Now) {Infrastructure(T) + Feature(T) + Defects(T)}

Okay we've mostly defined the problem space, but we haven't consider where **Testing** should go. Let's add it to the formula by weighting each Term with a coefficient.

If we include sufficient **Testing** with each **Feature**, we can assume our **Defects** will be reduced by say 50% and our cost to develop each **Feature** is increased by 100%. (Some case studies of TDD claim the number of lines of code for tests and business logic is equal!)

> \$Beta = Product(Now) = E(T=0, Now) {Infrastructure(T) + Feature(T) \* 2 + Defects(T) / 2 }

If we assume addressing **Defects** is significantly cheaper than developing **Features** and writing tests, so _\$Beta_ would be significantly more expensive than _\$Alpha_.

However, if we assume inadequate **Testing** is occurring, then we might reduce the **Feature** cost to the original in _\$Alpha_ and rely on our Customers and Support Tickets to determine when **Defects** were introduced to the system. We'll adjust _\$Alpha_ to reflect this and rename it as _\$Gamma_:

> \$Gamma = Product(Now) = E(T=0, Now) {Infrastructure(T) + Feature(T) + Defects(T) \* 2 }

So far _\$Gamma_ is the cheapest way to develop software! We should just never test until we find a **Defect** in the field!

However, we haven't accounted for the compounding technical debt and increased development time due to an _unstable and non-assertable_ codebase.

If we include the cost for context switching and debugging a misbehaving application that does not have a ground truth assertion to work with, a revised version of the formula might look like:

> \$Delta = Product(Now) = E(T=0, Now) {Infrastructure(T) + Feature(T) + Feature(T-1) / 2 + Defects(T) \* 2}

Oh no!!! We're paying more than full price for a **Feature**! And we've got twice the **Defects**!!

> \$Delta = Product(Now) = E(T=0, Now) {Infrastructure(T) + Feature(T) \* 1.5 + Defects(T) \* 2}

Lastly, let's consider the situation where **Features** rely on upon more than the previous **Feature**, and worst case **Feature(T)** relies upon **Feature(0...T-1)**.

> \$Eta = Product(Now) = E(T=0, Now) {Infrastructure(T) + Feature(T) + E(t=0, T-1) {Feature(t) / 2} + Defects(T) \* 2}

Now we're really in trouble, cost has entered in to realm of factorials.

We could add more coefficients to account for the introduced **Defects** found while maintaining the previous **Features**, but I think the point has already been made, cost model _\$Beta_ is cheaper.

With cost model _\$Eta_, the technical debt will quickly overwhelm us and soon we won't be able to make the minimum payment and our **Feature** development will grind to a halt.

The crux of the problem is that some teams treat testing as an after thought. The code is written, blessed, shipped, and tested. In that order, which only seems cost effective if you don't look at the entire picture of the **Product** over its lifecycle.

## Conclusion

My claim is that the _true_ cost to develop the **Product** is cheaper if **Testing** is done when the **Feature** is written. Defects never go away for free, which means you'll either be catching them while the **Feature** is in context or after it has been shipped and new **Features** are added to the dependency graph.

I've witnessed laborious human-based rituals performed on release candidates by teams of developers taking days (and even in some cases weeks) such that it may be proclaimed from the mountain tops to be defect-free. I will neglect to detail the frequency at which I've witnessed these rituals of sacred tribal knowledge be frantically repeated because a defect was introduced during the previous iteration of the ritual.

When one steps back, one must wonder "surely there is a better way, this can't be _the right way_, can it?" All we really want at the end of the day is to have confidence in our code and to avoid being called to address an outage in production on Friday at 7PM after having a beer.

In the case that my example of rituals and proclamations is too remote to identify with, I would challenge the reader to recall a time when they were writing code (whether it be fixing a bug, adding a new feature, or just messing around) and they had to conduct some arcane process to assert that the characters they just typed didn't cause the product to implode.

That feeling of discontent, of inconvenience, is the subtle cost of inadequate testing.

In _Part Two_ of this series I'll discuss ways to determine the value of a test, where to start on both new and not-new projects, and will provide a practical example of TDD in action.

If you found this post helpful or would like to fuel my caffeine addiction, [consider donating.](https://ko-fi.com/wghilliard)
