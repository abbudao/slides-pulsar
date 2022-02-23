# Introduction

Note:
My goal here is to motivate us, by telling a simple story on why using only the simple 
and traditional architecture of synchronous communication doesn't scale well as 
we grow up as a company.


## TOC

1.1 A new company is born

1.2 The monolith breaking you

1.3 Breaking the monolith

1.4 Why not synchronous communication?


## A new company is born

Note:
You are a Senior Developer, that had just quit your job and started a new Startup 
with your colleague, a successful business consultant.
And, Good news! You've just received funding for your new startup! And you start coding!


### Three tier architecture
![Three tier architecture](./slides/assets/three_tier_architecture.png)

Note:
Your architecture is simple, you have a pretty nice good frontend, consuming your backend, 
and you are evolving your product quite fast.

But a few months later, as your product was getting traction your company got big!

Dozens of software developers are now working on the codebase you once worked alone...


## The monolith breaking you

Note:
Not only you are having trouble developing features on the same repository of dozens of other developers,
but your company is also having a quite nice problem to have... New users are popping out of nowhere, but our servers 
are being overwhelmed. Something must be done...


### Vertical scaling
![Vertical Scaling](./slides/assets/vertical_scaling.png)

Note:
The most naive approach is just adding more resources to our machines. 
Getting beefier hardware is an option but keep in mind that we can't always get better
machines. They get more and more expensive and have physical scaling limitations.


### Horizontal scaling
![Horizontal Scaling](./slides/assets/horizontal_scaling.png)

Note:
On the other hand, we can always scale horizontally. Adding more machines will 
load balance our requests. But we can't choose what we want to scale!


### Monolith at scale
![Monolith](./slides/assets/monolith.png)

Note:
If we, for example, need to scale our application because we received too many orders,
we will waste resources because we also scaled unrelated components!

Or even worse! A critical part of your application might not be answering requests because the front page is being heavily
accessed on a marketing campaign.


## Breaking the monolith

Note:
We need to take action yet again...


![Microservices](./slides/assets/microservices.png)

Note: To tackle the scaling people and scaling machines problem,
you remembered how things were done in your old company. We did microservices, right?
We just need to split those modules into different applications!
Now we can scale out vertically or horizontally each application!


### Just break it on smaller apps, right?!


![Monolith](./slides/assets/monolith_entities.gif)
Note:
If we could represent the method calls of our monolithic application, it probably would look like this.
Even if we did our best efforts to not call methods unrelated to our modules, we inevitably ended up depending on some common code.


![Distributed Monolith](./slides/assets/distruted_monolith_entities.gif)
Note:
By naively breaking our monolith into small services, we ended up mimicking how our monolithic application worked, 
but now we've added latency between services. This is what we call a distributed monolith.

We ended with more hurdles than we had before.
You can see that for answering a single request, we probably depended on many other services.


<!-- .slide: data-background-color="white"  --> 
![Monolith Chart](./slides/assets/monolith_chart.png)

Note:
Although we had physically distributed our application in different places, we made no effort to decouple it logically.


## Why not synchronous communication?

Note:
Review what we had spoken about so far:

One of the big symptoms of having built a distributed monolith is having too many synchronous requests across services.

By analogy, it's like we were calling a remote method on our "distributed monolith". 

Synchronous requests are service coupling.

When we do things in this way, we have not only accumulated latency of communicating 
with many "microservices" but we also added the overhead of knowing how to communicate with them
(we need to know their addresses) and what they are expecting as requests (we need to know the routes schemas).

Not all workloads must be done immediately, but some must. Synchronous requests, as they are blocking, can be a good 
match for those immediate workloads, but maybe most of our workload can be in a non-blocking way, that I commit resources
just to get them faster, but it's also fine to keep it on a lower throughput if my product doesn't demand so.
