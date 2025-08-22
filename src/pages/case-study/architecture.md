---
layout: ../../layouts/CaseStudyLayout.astro
title: Architecture
description: Final review of Pendulum BaaS' architecture
prevSection: Design Decisions & Implementation Challenges
prevPath: /case-study/design-and-challenges/
nextSection: Future Work
nextPath: /case-study/future-work/
---

# Architecture

With design and implementation finalized, let’s take a look at Pendulum’s final architecture starting with the local development experience.

<h2 id="local-development">Local Development Experience</h2>

Our local development approach prioritizes developer simplicity. After initializing a project with **`npx pendulum init`**, developers start the entire backend with a single command: **`npx pendulum dev`**. This command installs the Pendulum SDK, initializes the development environment, and orchestrates all backend services.

Given our microservices architecture, Docker was our choice for local development. The backend consists of three containerized services orchestrated with Docker and connected via a bridge network:
- **MongoDB** with persistent volumes to maintain data across restarts.
- **App service** handling CRUD operations and serving the Admin Dashboard.
- **Events service** managing real-time connections via Server-Sent Events.

This containerized approach eliminates the need for developers to manually install and configure MongoDB, manage Node.js versions, or handle service dependencies. The isolated containers mirror our production architecture, ensuring alignment between the two environments.

<h2 id="production-architecture">Production Architecture</h2>

Looking at Pendulum’s production architecture, we continued to maintain the same philosophy that we set out with: provide developers with a simple, automated deployment process with a scalable production architecture. Production systems with solid architectures require load balancing, auto-scaling, managed databases, security groups, and monitoring — complexity that can overwhelm developers. Pendulum eliminates this friction through Infrastructure-as-Code automation using AWS Cloud Development Kit (CDK).

A single **`npx pendulum deploy`** command provisions complete production infrastructure in an isolated VPC in the developer’s AWS account.

<h3>Cloud Provider Choice</h3>

Building a BaaS platform with automated deployment leads to a fundamental choice: take the breadth-first approach of supporting multiple cloud providers or focus deeply on one and provide the best developer experience possible. Supporting multiple cloud providers offers vendor flexibility but significantly increases development complexity and maintenance overhead.

We chose an AWS-first strategy to prioritize developer experience over provider flexibility. AWS offers a robust ecosystem of managed services, extensive documentation, and the most widespread adoption of any cloud provider. We accepted the tradeoff of vendor lock-in for production deployments, but our open-source codebase enables users to adapt Pendulum for other providers if needed. For developers seeking rapid prototyping, the simplified deployment experience outweighs the loss of vendor flexibility.

<h3>Container Orchestration</h3>

As we discussed in reviewing our development architecture, we took the same containerized service approach for our production architecture. To handle container orchestration for scaling, networking, and deployment management, we evaluated three primary options:

**Elastic Kubernetes Service (EKS)** offers advanced features like custom resource definitions, advanced networking policies, and fine-grained resource management. However, it requires significant operational expertise, complex YAML configurations, and ongoing cluster management that conflicts with our zero-operations philosophy.

**EC2 instances** offer complete control over the runtime environment, allowing custom optimizations and direct server access. But this approach requires manual scaling, security patching, and infrastructure management that works against our goal of simple, automated deployment.

**Elastic Container Service (ECS) with Fargate** delivers serverless containers with automatic scaling, integrated AWS networking, and zero server management. While it sacrifices some flexibility and creates AWS vendor dependency, it aligns perfectly with our goal of eliminating operational overhead for developers.

We chose Fargate to provide a simple and scalable production architecture that requires little to no management from our end users. Both app and events services can scale independently, while AWS handles underlying infrastructure provisioning and management.

<h3>Database Selection</h3>

With MongoDB as the database for Pendulum, we could either choose to self-manage MongoBD on EC2 instances or go for the managed AWS DocumentDB service. DocumentDB integrates seamlessly with our existing MongoDB database operations, and offers managed scaling. On top of that, it offers automatic backups, replication across multiple Availability Zones, integrated security groups, and CloudWatch monitoring — features that would be difficult to replicate with a self-managed EC2 instance.

DocumentDB doesn't support all MongoDB features and creates further AWS dependency, but the alternative would require extensive expertise in replica set management, backup strategies, security hardening, and performance tuning.

<h3>Load Balancing and Traffic Management</h3>

Our microservices architecture requires rule-based traffic distribution and interservice communication. AWS’ Cloud Map lets us implement service discovery so that our backend services can communicate using logical names rather than hardcoded endpoints when containers scale.

For distributing frontend traffic, we used a two-tier approach: CloudFront handles SSL termination and global CDN delivery, forwarding to an Application Load Balancer (ALB) for service-specific routing. The ALB routes frontend requests based on path patterns to app and events service containers as well as admin dashboard resources.

This architecture creates a unified endpoint experience — CloudFront distribution behaviors enable the frontend SDK to seamlessly connect to appropriate backend services without additional developer configuration. Frontend applications deploy automatically to S3 with CloudFront distribution for global content delivery, while the ALB focuses on application-level routing and health checks.
