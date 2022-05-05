# Chaos Engineering with chaostoolkit on AWS

Why? http://events.smartwavesa.com/aws-reinvent-2017/chaos-engineering.pdf

...The first thing you need to do is decide what hypothesis you’re
going to test, which we covered in the section Chapter 4. Perhaps
you recently had an outage that was triggered by timeouts when
accessing one of your Redis caches, and you want to ensure that
your system is vulnerable to timeouts in any of the other caches in
your system. Or perhaps you’d like to verify that your active-passive
database configuration fails over cleanly when the primary database
server encounters a problem.

...
We believe that any organization that builds and operates a dis‐
tributed system and wishes to achieve a high rate of development
velocity will want to add Chaos Engineering to their collection of
approaches for improving resiliency

....

You break things in production (http://principlesofchaos.org/?lang=ENcontent) to prevent the black swans, the incidents
that will cost you 100,000s of $$$ (https://www.gremlin.com/community/tutorials/chaos-engineering-the-history-principles-and-practice/).

# So Let's Pick A Hypothesis

You run a distributed service, and your company just had an outage.
Visitors couldn't connect to your frontend, because some of the httpd containers
(e.g. in ECS) or
hosts (EC2 instances) crashed because some bug wrote the space full of logs.

Of course we could now do a bunch of things:

- we could fix the "bug", and write a test for it (or better first test, then fix)
- we could write an container level test to check that the logs cleaned if they
  are over 95% of space.
- ...

However we could also go a level higher, and simply test:

- What happens, when a container dies? What if two die? ...

The idea here is to test not for the known, but to prepare for the unknown.
Because there could be a million reasons a container dies, but only one of them
might be the "bug" we test for, only one is "the logs fill up the disc"...

That's what you aim for in chaos engineering.

# Intro

So while we want to test our hypothesis as quickly as possible, I do think you should
get to know both, the chaostoolkit, and the chaostoolkit-aws provider a little bit.
You can skip over the next two sections and go right into the actual hypothesis test
if you don't want to get into those details, or already know the chaostoolkit itself.

....

## Ressources

This is a hands on tutorial to teach you how to run a single chaos experiment
against your AWS tech stack. If you really want to start running chaos experiments
though, I'd urge you to read through:

- https://www.gremlin.com/community/tutorials/chaos-engineering-the-history-principles-and-practice/
- If you need more inspiration for attacks, check out those ones: https://www.gremlin.com/docs/infrastructure-layer/attacks/; I should note that gremlin provides great resources on chaos engineering.
