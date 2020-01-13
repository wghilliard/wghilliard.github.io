---
layout: post
title:  The Devops Handbook Review
date:   2020-01-12
categories: books development
---
At one point in time, you could have asked me, "Grayson,
how would you measure quality of a software product?" and I would have 
most likely answered with, "By how fast / accurate the code is!"

After a few years of working in various industry
environments, I have become familar with ways in which
a team might approach developing software. Sometimes
they focus on getting the MVP completed as fast as
possible, sometimes they want an MVP as cheap as
possible, and sometimes they want an MVP as good as
possible. However, it never occured to me that "good" was
really a component of cheap AND fast. It wasn't until I 
began reading "The Devops Handbook" that I realized 
that "good" was often thought of turning the "quality"
dial up [to 11](https://www.youtube.com/watch?v=s9F5fhJQo34).
However, I don't remember ever being asked the
question "How do you know you what you've built is good?"

Such a question could be interpreted as an accusation in 
some settings. In other settings it might be answered with slides and
graphs depiciting its performance over previous iterations or 
implementations. However another interpretation would consider
how _trustworthy_ it is, an incredibly important 
attribute that I now believe is _wildly_ underrated.

The Devops Handbook could be potentially summerized with
the following sentence:

"One cannot claim quality unless it is regularly asserted." 

These assertions can be executed in multiple ways:
- automated tests
- production telemetry

Automated testing allows an individual to claim with authority
that the thing they have built is _trustworthy_ and has _quality_.
An argument could be made that automated tests could be written in
such a manner that they are effectively meaningless, but I would
challenge the reader, for the sake of this post, to assume that 
an individual that was practicing this methodology 
put in the necessary effort to write meaningful and complete 
\<unit|integration|end-to-end> tests.

The Devops Handbook claims that such automated testing allows for
value streams to produce meaningful quality metrics and gives teams
a compass to determine if their development process is safe. These
tests would largely depend on the domain and architecture of the 
product in question, but if done correctly they decrease risk when
releasing the product, facilitate higher functioning workflows, and
give external (and internal) customers *faith* that the product will
work as intended.


