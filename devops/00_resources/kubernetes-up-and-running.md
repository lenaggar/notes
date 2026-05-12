# Chapter 1. Introduction

Main reasons to use containers or container api's like Kubernetes can be traced down to one of these benefits:
- Development velocity
- Scaling (software and teams)
- Infra abstraction
- Efficiency
- Cloud-native ecosystem

## Velocity

Users expect a reliable service more than iterative improvements.

> _"Velocity is measured not in terms of raw number of features you can ship per hour or day, but rather in terms of the number of things you can ship **while maintaining a highly available service**."_

Container and Kubernetes provide this through:
- Immutability
	It is important to have a _**record**_ of changes that are performed on a running container through creating a new immutable _**artifact**_.
	This way, it is possible to track what went wrong in case something breaks, and also have the ability to _**rollback**_ to a previous running deployment.
	Updating a live container should only happen in extreme cases when it is mission-critical and that this the fastest temporary repair and even then, the modification should be _recorded_ through a declarative config update after the fire is out.
- Declarative configuration
	_**Declarative**_ infra is less error-prone than _**Imperative**_ infra.
		_**Declarative**_ infra describes the desired state, the Kubernetes' job is to ensure that the actual state matches the desired state.
		_**Imperative**_ infra however, describes the execution steps that need to happen in order to reach the desired state.
	Storing declarative infra in code is referred to as _**Infrastructure as Code**_ or _**IaC**_. It eases code review and testing before deployment.
	_**GitOps**_ formalized _**IaC**_ making source control as the source of truth.
	In ***GitOps***, it is easy to ***rollback*** to a previous working state.
- Online self-healing systems
	Kubernetes does not only initialize the system's actual state to match the desired state, but rather it _continuously_ takes actions during operation of the system to ensure that the current state is matching the desired state, guarding against failures/disturbances that might affect the system reliability.
- Shared reusable libraries and tools

## Scaling (services and teams)

In order to benefit from Kubernetes' ease of scaling a system, the system must first be _**decoupled**_. There are two main ways to separate/isolate/decouple components:
- APIs
	Teams with defined APIs can have more focus and less cross-team communication overhead, reaching higher degree of autonomy.
- Load balancers
	Services capacity can increase without adjusting/reconfiguring any of the system's other layers.

Scaling applications and clusters with Kubernetes is easy.
Scaling applications is as simple as changing a number on a config file. This however assumes that there's always resources in the cluster available to be consumed. The cluster can be scaled by adding a new machine(s).
In the cloud, Kubernetes makes scaling up and down easy via _**Autoscaling**_ for both the applications and the cluster.

Scaling dev teams with microsevices:
- Ideal team size is 5~10 people (the two pizza team)
- To achieve agility and product end goals => service-oriented teams
- Each team is responsible for the design and delivery of a service that is consumed by other teams

Kubernetes provides abstractions to make it easier to build decoupled microservices architectures:
- Pods:
	group container images developed by different teams into a single deployable unit
- Kubernetes services:
	provide load-balancing, naming, discovery to isolate microservices
- Namespaces:
	provide isolation and access control so that each microservice controls degree which others interact with it
- Ingress:
	provide easy frontend/external API surface area

Kubernetes allows greater level of separation of concern, where:
- The Application engineer:
	- focuses on application SLA delivery
	- relies on the SLA delivered by Kubernetes
	- does not worry about the details of how this SLA is achieved
- The Kubernetes (container orchestration API) reliability engineer:
	- focuses on Kubernetes (container orchestration API) SLA delivery
	- relies on the SLA delivered by OS
	- does not worry about the details of how this SLA is achieved
- The OS reliability engineer:
	- focuses on OS SLA delivery
	- relies on the SLA delivered by hardware
	- does not worry about the details of how this SLA is achieved

This decoupling or clear separation of concern, allows each group to be a small team focusing solely on their own area of expertise, hence being more efficient.

_Note:_ The OS reliability engineer role in small/medium size companies can be simplified by relying on `KaaS` (Kubernetes as a Service) cloud solutions.

## Infra abstraction

Kubernetes, since being an application-oriented container orchestration API, can break teams out of the lock-in of certain cloud providers. Contrasting the usage of infra-oriented cloud APIs and cloud-specific services.

Moving towards application-oriented container orchestration APIs (such as Kubernetes) has two concrete benefits:
1. Separates developers from specific machines
2. Enables high degree of portability, since developers are consuming a higher level API that is implemented in terms of the specific cloud infra APIs
The caveat of course avoiding the usage of cloud-managed services and deploying and managing open source solutions instead.

So, building on top of Kubernetes application-oriented abstractions ensures that the effort you put into building, deploying, and managing the application is truly portable across a wide variety of environments.

## Efficiency

When using Kubernetes, multiple teams' output can colocate on the same machine, reducing the number of machines and eliminating the machine-per-team way of working.

> "Efficiency can be measured by the ratio of the useful work performed by a machine or process to the total amount of energy spent doing so."

> "Kubernetes provides tools that automate the distribution of applications across a cluster of machines, ensuring higher levels of utilization than are possible with traditional tooling."

> "a developer’s test environment can be quickly and cheaply created as a set of containers running in a personal view of a shared Kubernetes cluster (using a feature called `namespaces`)"

Increased ease of testing also directly increases velocity.

## Cloud-native ecosystem

Since its launch, Kubernetes (and Docker and Linux before it) was designed for extensibility and a broad welcoming community which lead to a large array of tools and services that have grown around it to the point that in many cases the challenge isn't finding a potential solution, but rather deciding which one of the many available solutions that fits the task.

The CNCF acts as industry home for cloud native projects.
There are three stages of project maturity:
1. The sandbox stage:
	early development, adoption not recommended unless early adopter or contributor
2. The incubating stage:
	proven utility and stability via adoption and production usage, however still in development
3. The graduated stage:
	fully mature, widely adopted

---
# 