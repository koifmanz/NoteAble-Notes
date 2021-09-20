---
tags: [Notebooks/AWS]
title: Cloud Computing
created: '2020-10-20T04:30:24.660Z'
modified: '2020-12-02T14:26:14.635Z'
---

# Cloud Computing

### What are the types of cloud computing?

* Infrastructure-as-a-Service (IaaS) - The provider supplies virtual server instances, storage, and mechanisms for you to manage servers. Rackspace for example (and somewhat AWS).
* Platform-as-a-Service (PaaS) - A platform of development tools hosted on a provider's infrastructure. GoDaddy for example.
* Software-as-a-Service (SaaS) - A software application that runs over the Internet and is managed by the service provider. For exmaple gmail or ms office 365.


### What are the types of deployment meodels?

* Public cloud - the resources (databases, servers, etc.) available over the internet. AWS is the largest today.
* Private / On-Premises - A private cloud is a proprietary network that supplies services to a limited number of people.
* Hybrid - a combination of both models. for example personal information will be Private, while web app to register will be public.


### AWS Global Infrastructure

* Region - a geogrphic area with availability zones within. 
* Availability Zone - an area is location within a region which have physical data center.
* Edge Location - mini-data center used solely to cache large data.

resources do not replicate across regions.

### Scaling Types:

* Vertical - modify the server, scaling him up by adding more memory and etc.
* Horizontal - add more nodes\servers, scaling out.
* Diagonal - a combination of the first two.

### Latency

The time that take to repsond to a request, the time from the access to the website until it load. high Latency is bad, A content delivery (CDN) can help with that. 


