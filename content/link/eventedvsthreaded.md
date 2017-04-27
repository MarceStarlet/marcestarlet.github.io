+++
author = "TechWo-MarceStarlet"
date = "2017-04-27T18:27:11-05:00"
ref = "https://blog.techwomen.org.mx/servidores-threaded-vs-evented-126a3388ae81"
title = "Evented vs Threaded"
type = "link"
+++

**Evented vs Threaded**

On this post I talk about the main differences between the Threaded and the Evented
models and how they work by doing an analogy of a real situation that easy explains
both models.

The **Threaded** model's analogy is about a bank and how the people is assigned to a
cashier, if the cashiers are busy then the people will start to queue, so this is how
the resources are blocked, until a cashier is free to atend a person, that resource or
thread is blocked. Wait is never confortable, and it could be a pain head if we want
to manage a thread pool since we never could know exactly how many threads will be
needed in a moment, this is also hard to scale vertically.

About the **Evented** model we can do an analogy of a butler in a mansion, taking all the
requests by the guests and delegating the tasks to the corresponding employeers in the
house like the housekeeper, the chef, the driver, gardener, etc. entrying in a loop on
its functionlaity, taking requests and delegating. Using an evented model we can avoid
the blocking resources due the butler or *event loop* is taking all the requests and
deligating them ASAP entrying in an asynchronous routine that allow us to continue the
code and receive the response of our request when is ready. It is easy to scale in the
code as well as the physical machines, vertically and horizontally.
