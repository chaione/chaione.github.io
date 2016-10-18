---
title: Overview
layout: default
---

# Overview

<p class="subtitle">Build contextual capabilities into your applications with just a few lines of code</p>

ContextHub provides a mechanism for third party developers to quickly and easily add powerful contextual capabilities to their applications with just a few lines of code. This enables developers to create unique and engaging experiences for their users.

ContextHub makes this possible through the following five major components:

2. **Event Services.** Establish interfaces with mobile devices and other smart objects, to allow easy collection of sensor data (GPS, motion, accelerometer, etc.). This allows their data and capabilities to become available not only locally, but remotely as well.
3. **Contextual Engine.** Provides developers with a central, cloud-based rules engine that responds to contextual events, with a context-aware language that allows triggering customized actions based on an evaluation of relevant data.
4. **Application Services.** Provide a set of convenient cloud-based services that facilitate development of contextual applications and reduce the need for developers to establish and manage a back-end scalable infrastructure of their own - for example, data storage (Vault) or push messaging (Push).</span>
5. **Analytics Services.** Provide a robust set of analytical capabilities for developers and administrators.

## Introduction
{: data-magellan-destination="introduction"}

The ContextHub service is available using the following tools:

- [iOS SDK](/docs/ios/)
- [Android SDK](/docs/android/)
- [REST API](/contexthub-api/)
- A [Developer Portal](/docs/admin/) for managing
    - [Vault data](/docs/admin/#Vault)
    - [Devices](/docs/admin/#Devices)
    - Creating and managing [Contextual Engine Rules](/docs/contextualengine/)
    - Custom event [Triggers](/docs/admin/#Triggers)
    - Reading [Analytics](/docs/admin/#Analytics) and [Logs](/docs/admin/#Logs)
    - Updating application [Settings](/docs/admin/#Settings)
- [Samples](/docs/samples/) and [Apps](/docs/apps/) the demonstrate features and functionality in action

This documentation will walk you though using the various components of ContextHub and contains examples of features and functionality. It is a work in progress, but we're working to quickly fill in the blanks.

## Getting Started
{: data-magellan-destination="getting-started"}

### Registration
On ContextHub, you create a separate app for each of your mobile applications. Each app has its own application id which you will use to register with the ContextHub SDKs and API. Each account on ContextHub can have multiple application ids for multiple apps. This lets you accommodate both testing and production versions of your app with the same account.

### Sign Up
[Sign up for ContextHub](https://app.contexthub.com) by either creating a username/password or using your [GitHub credentials](https://github.com/).
