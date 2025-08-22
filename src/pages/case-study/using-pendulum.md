---
layout: ../../layouts/CaseStudyLayout.astro
title: Using Pendulum
description: How to use the Pendulum BaaS Platform
prevSection: What is Pendulum?
prevPath: /case-study/what-is-pendulum/
nextSection: Design Decisions & Implementation Challenges
nextPath: /case-study/design-and-challenges/
---

# Using Pendulum

<h2 id="local-development">Local Development</h2>

Developers can get started building applications with Pendulum by developing locally. Simply create a project directory with the build tool of choice, move into the new directory, and install the Pendulum CLI.

Once the Pendulum CLI tool has been installed, running the `init` command installs the SDK and backend packages, and adds a couple helpful npm scripts for stopping and starting the backend.

The Pendulum SDK is easily incorporated into the frontend code with an import:

Developers can take advantage of both the default CRUD operations built into Pendulum, as well as the real-time data subscription feature to make frontend applications reactive. Here we look at both features at work in a React project using JavaScript.

On mount, we can fetch the items from the backend with a GET request. In that same effect we also subscribe to the “items” collection, passing in the `updateItems` function as the callback. Now, every time the events server pushes an update to the client, the `updateItems` function runs and updates the frontend state.

<h4>Starting the Development Environment</h4>

The `npx pendulum dev` command initialies the local development environment.

At any point during the development process, the Pendulum backend container network can be stopped or started with the npm scripts added during the `init` command.

The admin dashboard, available at **http:<span></span>//localhost:3000/admin** can now be used to manipulate backend data and visualize the flow of data through the application during local development. Additionally, developers can adjust collection-level permissions and observe these permission changes during runtime.

<h2 id="production">Production</h2>

When it’s time to deploy an application, executing the **`deploy`** command will prompt developers for their AWS account information, the desired region for deployment, the project name, and the path to the directory with their frontend build artifacts. The CLI tool will automatically deploy those resources, alongside the entire Pendulum backend infrastructure, to a dedicated VPC in the developer’s AWS account.

Conversely, deployments can be torn down and destroyed at any time with the **`destroy`** command. This command will destroy each AWS CloudFormation stack associated with the deployment.
