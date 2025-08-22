---
layout: ../../layouts/CaseStudyLayout.astro
title: What is Pendulum?
description: Description of Pendulum BaaS platforom
prevSection: Background
prevPath: /case-study/
nextSection: Using Pendulum
nextPath: /case-study/using-pendulum/
---

# What is Pendulum?

<h2 id="philosophy">Philosophy</h2>

The key tenet of a Backend as a Service is to abstract away backend implementation for developers — so why implement features that make developers write more backend-like code? With this philosophy in mind, we identified a few core features that would differentiate Pendulum from existing providers and suit our target user base:

<h3>Reactivity and Automatic API Endpoints</h3>

Some providers rely on real-time connections for all database operations. With Convex, for example, there are no automatically-generated API endpoints and users have to define a separate set of functions to be used for every database operation. This results in a lot of additional code that could potentially be handled by a single REST endpoint. The advantage of this is that a single connection can be used for both database operations and real-time updates. The result is faster data synchronization between the frontend and backend by avoiding the overhead of establishing new HTTP connections.

Despite the performance gain, we identified some drawbacks to this methodology for our intended use case. We anticipate that nearly all apps built with Pendulum will have some CRUD functionality, so we wanted to make performing standard database operations as easy as possible with little additional code. With Pendulum, developers get automatically-generated API endpoints for performing CRUD operations via standard HTTP requests and a single frontend method for subscribing to real-time data updates for reactive applications.

> <h4><em>Reactivity Explained</em></h4>
>
> We mention reactivity as a core Pendulum feature, but what does that really mean? The video below shows two separate clients interacting with a simple application built with Pendulum. As one client changes data (i.e., creates, updates, or deletes data), the other client sees this change reflected in their application in real time. **This is reactivity** - the frontend application *reacts* to changes in backend state so all active users get the most current data.

<h3>Automated Cloud Deployment</h3>

We wanted Pendulum to be easy to use so developers could quickly develop and deploy applications. With a simple set of terminal commands, Pendulum handles deploying frontend code alongside a scalable, containerized backend to an isolated VPC in the user’s AWS account. There, users manage application data through an intuitive dashboard where data lives entirely in their AWS account.

<h3>Flexible Data Schema</h3>

In the early stages of application development, the data model can be a bit unclear. Pendulum’s flexible data schema allows developers to start with simple schemas that can evolve organically as application requirements take shape.

<h2 id="core-components">Core Components</h2>

Now that we understand the use case for a BaaS platform, let’s look at Pendulum’s four core components:

<h3>Backend</h3>

The Pendulum backend is made up of two main services:

**Application Service**— Responsible for handling all CRUD operations, data validation, authentication, and authorization. This service exposes REST API endpoints for database operations, user management, and permission validation.

**Events Service** — A real-time events server dedicated to maintaining persistent connections with clients and distributing database change notifications to all subscribed applications.

<h3>Admin Dashboard</h3>

The admin dashboard is the developer’s window into the Pendulum backend. Developers can manipulate backend data, view real-time system logs, monitor database operations, and configure collection-level access controls all in one place.

<h3>Command-Line Interface (CLI)</h3>

The Pendulum CLI automates the entire development workflow. With four simple commands, developers can initialize a Pendulum-backed project, start the local development environment, and provision or teardown AWS resources in deployment.

<h3>Software Deveopment Kit (SDK)</h3>

Pendulum’s SDK is the interface to the Pendulum backend. Developers import the SDK client into their frontend code and instantiate a new instance of the `PendulumClient`. With this, a frontend application automatically connects to the Pendulum backend, and developers get access to methods for standard CRUD operations and real-time data synchronization.

Given our positioning in the BaaS landscape, here’s how Pendulum fits in:

<img
  src="/assets/background/existing-solutions-table-with-pendulum.svg"
  alt="Where Pendulum fits in to Existing BaaS Solutions"
/>
