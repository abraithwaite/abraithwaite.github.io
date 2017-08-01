---
layout: post
title:  "Your Kafka Consumers: A Metamorphosis"
date:   2017-07-31 23:59:59
categories: kafka linux operations
---

It's 4am Saturday.  You jolt awake to the blaring of an air raid siren.  You
make a mental note to change your pagerduty ringtone before logging in to see
that the data pipeline is fucked.  While working to find the root cause of the
lost messages and late deliveries, you consider selling everything you have and
starting a goat farm somewhere remote.  Hours after fruitless shuffling the
consumers have all caught up and producers are no longer dropping messages.  It
remains a mystery what caused the disruption but you know it's not a matter of
if, but when it will happen again.

This might be the thought process you've gone through being on point for
operating a Kafka cluster.  Fret not!  With a little diligence and a bit of
knowledge gained from this post we will make your life easier.

Many struggle with operating Kafka and it's not without just cause.  It's a
complex piece of software built to solve complex problems.  In my experience
operating Kafka clusters in the millions of events per second range, the
problem almost always was due to consumers, disk, or network.

Disk and network are always a challenge in heterogeneous environments so I'll
focus on consumers for now.  But first a bit of background.

## Background

Kafka relies on the pagecache for speed.  This has major implications for
Kafka's performance and reliability but it is also the root of the project's
success in my opinion.  The pagecache is what allows Kafka to be fast without a
ton of complexity in the code which surrounds disk access.  Instead the project
could focus on the harder problem of availability.

The drawback to using the pagecache is that it's one big shared pool for the
entire machine which it operates on.  While there are plenty of ways that you
can optimize the pagecache, the easiest is simply isolating Kafka from other
services.

*Making sure the pagecache stays hot is the most critical piece of
maintaining a healthy Kafka cluster.*

Isolating Kafka to dedicated machines is sometimes enough, but oftentimes it
is not.  The other big pagecache polluter are the Kafka consumers themselves.

## How consumers affect the pagecache

Hopefully it doesn't come as a surprise that the number one offenders to
pagecache cache misses are consumers.  Just a few slow consumers which
continually miss the pagecache can significantly impact the performance of your
cluster.  Unfortunately, consumers are frequently overlooked as something
important to monitor for the health and stability of the Kafka cluster.

I believe that more often than oversight team organization is at fault for this
imbalance.  Kafka will often be managed by infrastructure teams who don't have
a strong say in what consumers can consume from the cluster.  In any case, the
second most important thing to monitor is consumer lag (after under-replicated
partitions).  Under-replicated partitions indicate something is definitely
wrong so always investigate the cause of those.  Consumer lag results in
pagecache pollution, so could cause a cascading degraded state in your cluster
as more and more consumers are unable to find cache-hits.

The best response to lagging consumers is to stop them if it's an option.  I've
put in policies that no consumer be added to a cluster which couldn't keep up
with the topic they consumed for a continuous period of time, usually at least
24 hours of normal traffic.  This can be tricky since it's possible for
consumers to connect and start consuming without saving their offsets in
zookeeper.  Kafka doesn't expose any kind of message or metric to inform us of
what consumers are connected so the best you can do is simply being strict
about the policy that no consumer gets added to production without monitored
offset tracking.

Another strategy I used in production was to closely monitor the disk io stats.
I'm not talking about alerting on high IOPs, but instead I watch the read
bandwidth and know that if it shoots up for a period of time and there aren't
any lagging consumers, then we've got a rogue consumer.  This only works after
you've started to track and monitor the individual consumer lag.  It also is
dependent on your workload.

If replays and rewinds are a fundamental part of your workload, then I suggest
a slight tweak to your architecture to support two tiers of service.

## Architecture

The concept of a set of tiered Kafka clusters isn't exactly new.  However, it
can greatly impact your ability to manage consumers if you implement it early.
If you're in the cloud, it's quite easy.  Basically, it's good to have one
ingest cluster which can serve real-time consumers and sub-topics and another
cluster to handle rewinds, backfills, and new consumer testing.

Additionally, it's good practice to have a service sit in front of Kafka to
ingest messages before they get produced to Kafka.  This allows easier
monitoring of what clients are producing to which topics.  Once again, Kafka
itself is lacking in this area of monitoring.  Furthermore, having a front-end
tier means that you can buffer incoming requests without blocking other
applications or services trying to produce to Kafka.

One issue you might run into with a tiered Kafka is that it's often very useful
to have a mapping between the upstream and downstream topic offsets.  If you
use consistent hashing, this shouldn't be terribly difficult to choose offsets
to start your downstream topic at, maintaining the continuous mapping.  To get
back to the original offsets, simply add the offset you started consuming from
in the upstream topic to the current offset of the downstream topic.

Finally, large Kafka clusters should be organized according to product area.
This goes along with the usage patterns above but in addition to that it also
provides clean separation of failure domains.  e.g. Your systems Kafka cluster
going down doesn't impede your webapp's ability to deliver messages to clients
and vice versa.  This is also generally good systems design advice, but
deserves to be called out here because it will cost more money.

## Kafka Summit

The San Francisco Kafka Summit is coming up.  I will not be attending but if
you are, I'd love to speak with you when you're in town.  Kafka's not
particularly revolutionary software, but it is the current best queuing system
out there.  Trying to do the same thing in Amazon's Kinesis or SQS would cost
millions of dollars per-month!  So if you're interested, reach out to me via
any of my contact points.

Some links:

https://kafka.apache.org/documentation/#design
http://duartes.org/gustavo/blog/post/page-cache-the-affair-between-memory-and-files/
https://www.thomas-krenn.com/en/wiki/Linux_Page_Cache_Basics
https://kafka-summit.org/events/kafka-summit-sf/
