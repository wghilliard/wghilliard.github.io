---
layout: post
title: Book Review - The DevOps Handbook
date: 2020-01-12
categories: books development
---

WIP Disclaimer - All content is subject to change!

---

At one point in time, you could have asked me, "Grayson,
how would you measure quality of a software product?" and I would have
most likely answered with, "By how fast / accurate the code is!"

After a few years of working in various industry
environments, I have become familiar with ways in which
a team might approach developing software. Sometimes
they focus on getting the MVP completed as fast as
possible, sometimes they want an MVP as cheap as
possible, and sometimes they want an MVP as good as
possible. However, it never occurred to me that "good" was
really a component of cheap AND fast. It wasn't until I
began reading ["The DevOps Handbook"](https://www.amazon.com/dp/B01M9ASFQ3)
that I realized that "good" is usually often thought of as turning the "quality"
dial up [to 11](https://www.youtube.com/watch?v=s9F5fhJQo34), where some algorithm
performs faster or the product is more feature complete.
However, I seldom remember being asked the
question "How do you know you what you've built is good?"

Such a question could be interpreted as an accusation in
some settings, with ones rapport being questioned. In other settings it might be 
simply answered with slides and graphs depicting the product's performance over 
previous iterations or implementations. However another interpretation would 
consider how _trustworthy_ the product is, an incredibly important
attribute that I now believe is _wildly_ underrated.

The DevOps Handbook could be potentially summarized with
the following sentence:

>One cannot claim quality unless it is regularly asserted.

These assertions can be executed in multiple ways:

- Automated Testing
- Production Telemetry

### Automated Testing

Automated testing allows an individual to claim with authority
that the thing they have built is _trustworthy_ and has _quality_.
An argument could be made that automated tests could be written in
such a manner that they are effectively meaningless, but I would
challenge the reader, for the sake of this post, to assume that
an individual that was practicing this methodology
put in the necessary effort to write meaningful and complete < unit | integration | end-to-end > tests. (1)

The DevOps Handbook claims that such automated testing allows for
value streams to produce meaningful quality-metrics and gives teams
a litmus test to determine if their development process is safe. These
tests would largely depend on the domain and architecture of the
product in question, but if done correctly they decrease risk when
releasing the product by revealing bugs early on, facilitate higher functioning
workflows (measured by lead time), and give external (and internal) customers
_faith_ that the product will work as intended when it is delivered.

Some environments see an investment in to automated testing as a _nice to have_
almost as if it were a feature to be implemented in the next major release. However,
this perspective trivializes the costs associated with last minute refactoring,
emergency hot fixes, and most importantly - brand degradation. A deficit of
automated testing leads to product accruing a compounding mountain of technical
debt resulting in a codebase so fragile and mystifying that even senior engineers
might wonder how the product even worked in the first place. Spooky. (2)

So, enough with the war stories, let's pretend we've got automated testing!
Depending on the VSC flow the team is using, "quality gates" can be constructed
that give the team (and all other downstream consumers) _*faith*_ that the product
will do everything it claims to do. (3) These gates can be arranged such that the
intensity and scope increase with each level as described below:

| Gate Number | Examples    | Run Time |
| ----------- | ----------- | -------- |
| 1           |type checking, linting | milliseconds to seconds
| 2           |unit tests - known IO, light mocking, accurate   |seconds to minutes|
| 3           |integration tests - module composition, heavy mocking, behavioral| minutes to hours|
| 4 | end-to-end tests - no mocking, "real" services, api or ui driven, small data sets| minutes to hours|
| 5 | performance tests - similar to end-to-end but with larger data sets| minutes to hours|
| 6 | manual testing - human + checklist driven| minutes (4)|

The above gates are just a guideline, make it makes sense to mix and match for a given product due to the domain, team, technologies, etc.

### Production Telemetry

Production telemetry helps answer the question "Is what we delivered providing value to
the customer?" Without a mechanism to determine if a feature is providing value to the
customer in an objective fashion, developers (and UX, QA, etc.) are left with anecdotes
to describe the customers satisfaction or dissatisfaction. Naturally only the extrema of
the feedback is reported and the development is guided by the outliers. Should time and 
energy be allocated to rebuilding / improving a certain feature? How do we know that the 
investment will provide value if we have no way to determine if our customers find that 
feature valuable? Moreover, the team is not empowered to experiment because it is 
arguably impossible to determine if a given change will improve or disrupt a customers 
workflow within the product. Therefore, instrumenting the product will give the 
development team visibility in to how the product is being used, and will objectively 
assert whether or not value is being provided. (5)

Footnotes:

1. Some real-world architectures and brown-field projects make certain types of
testing a seemingly insurmountable task.
2. If there are no tests to assert quality / desired behavior and a "bug" is found, is it really a bug?
3. Or at least what the tests claim the product can do.
4. Ideally human testing is reserved for edge cases and difficult to reproduce scenarios, but this isn't always the case.
5. Sometimes it's not possible to derive a metric from aesthetic things, e.g. font or
page layout. In this case A/B testing can be used to help answer questions about qualitative features.
