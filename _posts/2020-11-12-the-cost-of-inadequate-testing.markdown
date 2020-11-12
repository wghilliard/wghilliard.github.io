---
layout: post
title: Opinion - The Cost of Inadequate Testing
date: 2020-11-12
categories: opinion development
---

WIP Disclaimer - All content is subject to change!

---

# The Cost of Inadequate Testing

Often I find that the value of testing is difficult to measure, however the cost of inadequate testing is quite pronounced.

There are many projects out there, all with constraints and caveats that make test strategies arguably unique. One might claim that common layers of the stack can be addressed in common manner. For example modern HTTP web servers often include a testing framework, and special runtime environments like Android or iOS have frameworks that provide conventional patterns to setup the environment and make assertions.

However, something that often goes unconsidered is the cost of the tests written and the value they provide.

For instance, one might invest a substantial amount of time writing extensive tests to ensure line (and branch) coverage of given component, only to find bugs appear in production in adjacent components, or worse the component is refactored and the tests become obsolete.

In this situation, someone like Kent Beck (author of Test-Driven Development by Example) would argue that the tests were flawed from the start because changes in implementation details should not affect the tests. I'd allege he'd go on to say that the production bugs would have been caught if time was spent adding more contract tests to the adjacent components instead of testing implementation details, or if TDD was used from the start.

However it seems like other extrema of testing is more prominent - an after thought. The code is written, blessed, shipped, and tested. In that order.

I've witnessed laborious human-based rituals performed on release candidates by teams of developers taking days (and even in some cases weeks) such that it may be proclaimed from the mountain tops to be bug-free. I will neglect to detail the frequency at which I've witnessed these rituals of sacred tribal knowledge be frantically repeated because a bug was introduced during the previous iteration of the ritual.

When one steps back, one must wonder "surely there is a better way, this can't be _the right way_, can it?" All we really want at the end of the day is to have confidence in our code and to avoid being called to address an outage in production on Friday at 7PM after having a beer.

In the case that my example of rituals and proclamations is too remote to identify with, I would challenge the reader to recall a time when they were writing code (whether it be fixing a bug, adding a new feature, or just messing around) and they had to conduct some arcane process to assert that the characters they just typed didn't cause the product to implode.

That feeling of discontent, of inconvenience, is the subtle cost of inadequate testing.

## Risk

An old adage in software goes something like "make the common case fast", however it's probably worth adding "and stable". One could interpret this amendment in a few different ways.

### Only test the code that gets called 80% of the time

One way of assessing risk is understanding the common code paths that your product uses and writing tests to cover them. Writing Sock Shop? Then unit / integration / smoke / ui tests should ensure that the user can add socks to their cart.

### Only test the happy path

When writing a new interface, it's the perfect opportunity to add happy path tests to assert that the defined contract is satisfied by the implementing classes. If things like index errors are never really encountered because you're using functional programing techniques, then maybe that IndexOutOfBounds test isn't very valuable.

### Keep the dev loop __fast__

I prefer this interpretation to the others because it promotes the notion that confidence in one's product should be assert-able in a moments notice. Imagine being on a tech support call with a customer and DM'ing a developer to ask "are null values allowed in the XYZ table?" and the developer responds with, "brb I need to deploy the product to staging to find out". Scenarios like this devalue the time of the developer, degrade the trust of the customer, and are expensive in terms of opportunity cost for the company.

I believe, as a developer, the less time I spend mind numbingly pulling levers and turning dials, the better.

Some may claim, "But Grayson! My situation is different! My product runs in an environment that is non-conducive to testing and I can't afford to invest in building a custom test harness!" This line of thinking fails to consider the long term maintenance costs of the product and the human nature of developers. If they must conduct a monotonous sequence of actions in order to assert the quality of the features, one will soon find that cost-estimates for features now must account for not only the manual cost of testing the old features __but also__ the cost of manually testing the new features. By not investing in a test harness, one exposes themselves to substantial risk of linearly increased development and maintenance costs. Oh, and developer burn out. Do you _really_ want to type that default password in to the login page? Or click through that first-time-experience dialog?

It's worth noting that development costs may not be affected if engineers find the using the manual testing strategy too laborious and omit it from the dev loop entirely. One may find the total cost has not changed, but rather the development cost has merely shifted to the maintenance column due to the increased rate of production bugs introduced when untested code gets shipped.

Lastly, the risk of shipping test-able bugs is proportional to the number of manual test sequences, meaning the longer one waits - the worse it gets.

## Creating New Things

Though old habits and lethargy some times make it challenging, I find myself often attempting to write tests _before_ writing the feature code. Yes, yes, Kent would be proud that I'm drinking the punch. However I would invite you consider the situation of "The Unwritten Interface":

There are moments when building a product that a developer gets to create something new, to conjure something from thin air. In the land of test cases, the canvas is blank, the pallette undefined, and the brush in hand. In this realm, the developer is free to dream and to unleash their abundant creativity in order to craft something worthy of sacrificing to the alter of all that is good and beautiful.

There's a small caveat - whatever is good and beautiful may not compile, but for now that's okay.

Techniques like Test-Driven Development (TDD) give the developer room to run and experiment with what feels and looks right. Unconstrained by dependencies, control flow, or the call stack.

In order to get things to compile, whatever hasn't been defined can be stubbed and dependencies can be mocked. This freedom allows one to broaden their perspective of the problem in order to arrive at a solution without being burdened by the blinders of convention.

Once the solution is found and the test result turns green, one can start to replace mocks and stubs with real implementations in an incremental fashion such that the nature of the interface is preserved.

Then once the base case is working, they may move on to exercising the interface further, adding test cases and refactoring the design as appropriate.

In comparison, one could also design the interface _in the codebase_ in the land of _what is_ and _what works_, however they run the risk of over-fitting the solution to the problem and their time spent designing may be doubled if they failed to make the interface testable and therefore in need of a refactor when the tests are eventually written.

## Conclusion

Though the upfront cost of testing a product may seem expensive, it is important to consider the installments paid every time _that one feature_ needs to be worked on or a bug is found in production shortly after releasing. Having confidence in the product and fast dev loops is sometimes worth the overhead of investing in tests and test-driven development.

_If it means there's a better chance one won't get called at 7PM on a Friday after having a beer, it's worth trying right?_

## Further Reading

- Test-Driven Development By Example - Kent Beck

If you found this post helpful or would like to fuel my caffeine addiction, [consider donating.](https://ko-fi.com/wghilliard)
