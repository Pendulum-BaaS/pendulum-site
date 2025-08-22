---
layout: ../../layouts/CaseStudyLayout.astro
title: Background
description: Backend as a Service Background
nextSection: What is Pendulum?
nextPath: /case-study/what-is-pendulum/
---

# Background

<h2 id="intro">Introduction</h2>

Pendulum is an open source Backend as a Service (BaaS) platform built with solo and small development teams in mind. Pendulum enables developers to quickly prototype and build web applications where frontend data is synchronized to backend state in real time and automated deployment to an existing AWS account is handled with a single command.

<h2 id="cloud-service-models">Cloud Service Models</h2>

Building and deploying web applications and managing infrastructure can be complicated. As web development has progressed, developers have sought out ways to reduce this complexity to focus more on application logic and user experience. Numerous products and services exist to solve this problem, and three main service models have gained prominence, each sacrificing developer control for increased simplicity.

<h3 id="iaas">IaaS (Infrastructure as a Service)</h2>

AWS, GCP, and Azure provide compute, storage, and networking resources without requiring physical hardware management. Developers maintain control over operating systems, runtime environments, and application infrastructure while the provider manages the hardware.

<h3 id="paas">PaaS (Platform as a Service)</h2>

Platforms like Heroku, Fly.io, and Render abstract away infrastructure provisioning, load balancing, and scaling. By managing these components, developers can worry less about infrastructure and deployment while maintaining control over data stores and application code.

<h3 id="">BaaS (Backend as a Service)</h2>

Services like Convex, Firebase, and Supabase build off of IaaS and PaaS platforms and also handle typical backend services like creating API endpoints and database management. With BaaS, developers focus primarily on frontend code and connect to the managed backend through the platform’s SDK.

<img
  src="/assets/background/cloud-platform-comparisons.svg"
  alt="Cloud Platform Comparison"
/>

<h2 id="modern-web-application-structure">Modern Web Application Structure</h2>

Before continuing into Backend as a Service platforms, it’s important to consider how most modern web applications look today:

The **frontend** is the **Presentation tier** of an application. Static files run in the browser to control the user interface and make API requests to the Application tier for fetching and sending data. The **backend** of an application incorporates both the **Application** and **Data** tiers. It handles frontend requests, executes business logic, and manages storing and retrieving data.

<h2 id="use-case-for-baas">The Use Case for BaaS</h2>

With this web app structure in mind, the use case for BaaS platforms becomes clear; infrastructure and deployment aside, building full stack web applications is complex! Developers who want to prototype applications quickly and build great UI’s are bogged down with backend implementation details — many of which are the same across projects. Backend as a Service platforms offer a variety of backend features so developers can focus on what’s most important to them.

<h3>Convex</h3>

Convex is a reactive database that also acts as a BaaS platform for building applications. With Convex, database schema, queries, and mutations are defined using TypeScript functions and all database operations are performed through server-side functions that provide real-time synchronization of application state. Convex also handles configuration and deployment of backend services like user authentication and file storage.

<h3>Firebase</h3>

Firebase is a BaaS platform from Google that provides developers with a fully-managed backend infrastructure for prototyping and building applications quickly. It uses a NoSQL database and offers real-time updates.

<h3>Supabase</h3>

Supabase is an open-source alternative to Firebase that allows developers to easily build and manage the backend of their applications. One of its primary differentiating factors is its use of PostgreSQL, which makes it ideal for applications with a well-defined data model.


<img
  src="/assets/background/existing-solutions-table.svg"
  alt="Existing BaaS Solutions"
/>
