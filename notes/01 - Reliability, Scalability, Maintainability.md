---
tags: [Notebooks/DesignDataApp]
title: '01 - Reliability, Scalability, Maintainability'
created: '2021-09-07T05:05:42.796Z'
modified: '2021-09-20T05:58:56.399Z'
---

# 01 - Reliability, Scalability, Maintainability

### Reliability?

continuing to work correctly, even when things go wrong. The things can go wrong are called faults, and they are not the same as failure. The former is one componenet defiating from its spec, while the latter is when the all system as a whole stop. 
In general, it can be useful to increase the rate of faults by triggering them deliberately, to test the system.

#### Types of faults

* Hardware - as for today there are move to systems (like aws) that can tolerate the loss of entire machine. This types of faults are usually not correlated or have a weak correlations between them.  
* Software - error within the system, with higher correlations across nodes. It is important to do a lot of testing.
* Humans - we are making mistakes, and a lot of them. To solve the humans problem one can:
  * design a system that minimizes opportunities for error (like well-designed API)
  * create sandbox that are not affect real data
  * Test thoroughly at all levels, from unit tests to whole-system integration tests and manual tests
  * Allow quick and easy recovery from human errors, to minimize the impact in the case of a failure. For example, make it fast to roll back configuration changes
  * Set up detailed and clear monitoring, such as performance metrics and error rates
  * Implement good management practices and training


### Scalability?

Scalability is the term we use to describe a system’s ability to cope with increased load. If a system is working reliably today, that doesn’t mean it will necessarily work reliably in the future. One common reason for degradation is increased load: perhaps the system has grown from 10,000 concurrent users to 100,000 concurrent users, or it is processing much larger volumes of data than it did before.

#### Load?

Load can be described with a few numbers which we call load parameters. The best choice of parameters depends on the architecture of your system. For example:

* requests per second to a web server
* the ratio of reads to writes in a db
* the number of simultaneously active users in a chat room
* the hit rate on a cache

#### Performance?

Once you have described the load on your system, you can investigate what happens when the load increases. There are two ways to look at it:

1. increase a load parameter and keep the system resources unchanged (twitter: more follower to update home, while the same CPU, etc.)
2. increase a load parameter, and how much do you need to increase resources so the performance won't change. 

In a batch processing system such as Hadoop, we usually care about throughput—the number of records we can process per second, or the total time it takes to run a job on a dataset of a certain size. In online systems, what’s usually more important is the service’s response time—that is, the time between a client sending a request and receiving a response.

A good way to measure it is using median with percentiles, on the client side. On the server side you will not be affected by queueing delays. When testing send requests without waiting for the former request.

#### Coping with Load

* Scaling up - vertical scaling, moving to a more powerful machine.
* scailng out - horizonal scaling. distributing the load across multiple smaller machines.

In reality, good architectures usually involve a pragmatic mixture of approaches. for example, using several fairly powerful machines can still be simpler and cheaper than a large number of small virtual machines.

* Elastic - a system that can add computing resources when they detect a load increase. 

Elastic system can be useful if load is highly unpredictable, but manually scaled systems are simpler and may have fewer operational surprises.

### Maintainability

the majority of the cost of software is not in its initial development, but in its ongoing maintenance—fixing bugs, keeping its systems operational, investigating failures, adapting it to new platforms, modifying it for new use cases, repaying technical debt, and adding new features.

three design principles for software systems:

* Operability - Make it easy for operations teams to keep the system running smoothly
* Simplicity - Make it easy for new engineers to understand the system, by removing as much complexity as possible from the system. A abastraction is usually the answer here.
* Evolvability - Make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change. Also known as extensibility, modifiability, or plasticity.













