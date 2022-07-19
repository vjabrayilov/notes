---
title: "Serverless Computing"
date: 2022-07-19T14:59:06+04:00
draft: false
tags: [serverless]
---
## Introduction
* Serverless computing delivers *true* pay only for resources used with almost infinite scalability. 
* Customers will only focus on the business aspects of their applications. Developers do not need to to worry about low-level details of servers management and scaling, and only pay for when processing requests or events.
* **Definiton**: Serverless computing is a platform that hides server usage from developers and runs code on-demand automatically
scaled and billed only for the time the code is running.
* Sometimes zero scaling is not possible, a minimum memory and CPU allocation can be required and there are ongoing costs. Like Amazon Aurora
* FaaS (Function-as-a-Service) focuses on small pieces if code represented as functions to run for limited time and triggered by events or HTTP requests. It is not allowed to keep persistent state.
  * **Definition:** Function-as-a-Service is a serverless computing platform where the unit of computation is a function that is executed in response to triggers such as events or HTTP requests.

## History and Related Work
* Serverless builds upon long-running trends and advances in both distributed systems, pub/sub systems and event-driven programming models, including actor models, reactive programming, and active db systems.
![comparison of XaaS](/static/serverless-comparison.png)

## Further read
- [ ] https://pauldjohnston.medium.com/a-simple-definition-of-serverless-8492adfb175a
- [ ] http://bit.ly/2xzNEWB
- [ ] 
## References
- https://dl.acm.org/doi/pdf/10.1145/3368454
