---
tags: [Notebooks/AWS]
title: Networking & Elasticiy
created: '2020-10-20T13:06:27.442Z'
modified: '2020-10-20T13:27:50.980Z'
---

# Networking & Elasticiy

### Why Networking?

Networks reliably carry loads of data around the globe allowing for the delivery of content and applications with high availability. The network is the foundation the infrastructure. 

Cloud networking includes:

* network architecture
* network connectivity
* application delivery
* global performance
* delivery

Route 53 is a AWS cloud domain name system (DNS), service that has servers distributed around the globe used to translates human-readable names like www.google.com into the numeric IP addresses like 74.125.21.147.

* scales automatically to manage spikes in DNS queries
* allows you to register a domain name (or manage an existing)
* routes internet traffic to the resources for your domain
* checks the health of your resources


### Why Elasticity?

One of the main benefits of the cloud is that it allows you to stop guessing about capacity when you need to run your applications. With **elasticity**, your servers, databases, and application resources can automatically scale up or scale down based on load.

In *Amazon EC2* scaling up (or vertically) can easily be achieved by stopping an instance and resizing it to an instance type that has more RAM, CPU, IO, or you can scale out (or horizontally), which increases the number of resources. An example would be adding more servers.

EC2 also have **Auto Scaling**, which is is a service that monitors your EC2 instances and automatically adjusts by adding or removing EC2 instances based on conditions you define in order to maintain application availability and provide peak performance to your users.

### Elastic Load Balancing

Elastic Load Balancing automatically distributes incoming application traffic across multiple servers. Elastic Load Balancing works with EC2 Instances, containers, IP addresses, and Lambda functions.
it useful for the follwing:

* Balances load between two or more servers
* Stands in front of a web server
* Provides redundancy and performance

**Redundancy** is if lose a server the load balancer will send requests to the other servers. **Performance** is when the server having issues or bottlenecs, the load balancer will add more servers to the pool. The auto scaling will adjust the capacity to maintain a steady state.

<p align="center">
  <img src="https://i.imgur.com/Zhs0lvW.png" width="700">
</p>

