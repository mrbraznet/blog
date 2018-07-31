---
layout: post
title:  "How to be more productive on microservices development?"
categories: Microservices
excerpt_separator: <!--more-->
---
Everyone that started to use microservices end up with a huge problem: 

>Each microservice should have a set of capabilities.

And the list is not short.<!--more--> It includes capabilities like Discovery, Invocation, Elasticity, Resilience, Logging, Monitoring, Tracing, Pipeline, Authorization and API.

In the early adoption of microservices as a part of your architecture, you had almost nothing related to solve those capabilities. So it was responsibility of developer to solve these problems. The most famous case of this is the Netflix OSS.

> So, what is the problem with this approach? 

The problem is that you have business logic and network functions mixed into your code and it turns reading, understanding and maintaining, an stressful work.

![The problem of libraries to solve capabilities](/assets/images/posts/network-commingled.png)

Another problem is the size of the container image, because you are using libraries as dependencies and they are incorporated in the final installation package.

> Are you, as a developer, feeling that you are doing much more work now?

So, think for a while and ask yourself: Why I am doing this kind of control in my code? Is it really necessary?

Let's review the capabilities that was commonly solved using the code, and see how you can remove it.

# Service Discovery

One good solution for Service Discovery is to use all of the following components together: 

* Service Registrar 
    * <a target="_blank" href="https://github.com/netflix/Prana">Prana</a>
    * <a target="_blank" href="https://github.com/gliderlabs/registrator">Registrator</a>
    * <a target="_blank" href="https://github.com/airbnb/nerve">Nerve</a>
* Service Registry
    * <a target="_blank" href="https://github.com/Netflix/eureka">Eureka</a>
    * <a target="_blank" href="https://github.com/coreos/etcd">etcd</a>
    * <a target="_blank" href="https://www.consul.io/">Consul</a>
    * <a target="_blank" href="http://zookeeper.apache.org/">Zookeeper</a>
* Proxy
    * <a target="_blank" href="https://www.nginx.com">NGINX</a>
    * <a target="_blank" href="https://aws.amazon.com/elasticloadbalancing/">AWS Elastic Load Balancer</a>
    * <a target="_blank" href="https://www.envoyproxy.io">Envoy</a>
    * <a target="_blank" href="https://github.com/airbnb/synapse">Synapse</a>

![Service Discovery Solution](/assets/images/posts/service-discovery.png)

<a target="_blank" href="https://github.com/kubernetes/kubernetes/blob/master/docs/design/architecture.md">Kubernetes</a> have the Service Discovery built-in and it uses the etcd to do it. <a target="_blank" href="http://aws.amazon.com/documentation/ecs">Amazon ECS</a> has its own solution for Service Discovery also.

# Resilience

Resilience is achieved by using Circuit Breaker pattern. The most common solution is the Histryx by Netflix OSS. Again, if you are using a proxy for inter services communication, why not let the proxy to manage it for you? <a target="_blank" href="https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/circuit_breaking">Envoy</a> and <a target="_blank" href="https://www.nginx.com/blog/microservices-reference-architecture-nginx-circuit-breaker-pattern/">NGINX</a> has the built-in circuit breaker pattern.

> Maybe, you are asking yourself now: So, what is the point? Why should I change my code in order to incorporate this kind of infrastructure?

Because you are producing microservices and probably you want to experiment some another languages and platforms, so instead of having to build a lot of code for each language or platform, you delegate it to the infrastructure. 

Microservices architecture is not easy to accomplish, so you have a lot of complexity to deal with. Implement and follow up with infrastructure capabilities, is the easiest way to deal with it.

# API

By far, manage inter service communication is the hardest job ever in a microservices architecture. Because you have a lot of protocols you can use for each problem you have. 

The most used communication model is REST, but I ask you: Is it the best choice for all the requirements, problems and scenarios you have? It is a broad discussion, right?

Because of this, I am inviting you to join me and another developers in the live webinar that is called  **How to choose the right protocol for each problem you have?**. 

This live webinar is an start point for the **Microservices Straight from the Trenches Series**. In this series we will be discussing about real problems in real projects. You can grab your own questions and problems and iteract with us.

It is a special content that is only available for developers that is subscribed to my list. So, if you are not a subscriber yet, it is time to do it now, just leave your best e-mail address and join hundreds of developers to get exclusive contents and with priority.

<p class="text-center">
    <a target="_blank" href="https://webinars.mrbraz.tech" class="btn btn-lg btn-primary">I wanna join now!</a>
</p>

There are anothers capabilities to get out from your code, but I think you have a lot of information in this post to research on. As I wrote before, we are starting a new series and much more will come.

In the next series post we will discuss about Authorization and Logging, so stay in tune. If you wanna be notified when a new content is available for you, don't forget to subscribe to the newsletter list and to join me in the social media.
