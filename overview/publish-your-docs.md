---
icon: memory
---

# Architecture

{% hint style="info" %}
This page describes the project's technical grid and how it works.
{% endhint %}



## Overview

This project is designed as a web service, allowing users to submit a Pool Key from Uniswap V4 and choose between dynamic and static analysis options. Users can access this service via a web interface. When a Pool Key initialized in the Uniswap V4 Pool Manager is provided, the system begins its analysis based on this Pool Key.

<figure><img src="../.gitbook/assets/master_page_m – PF - 2 (2).png" alt="" width="563"><figcaption></figcaption></figure>

The Pool Key information is stored in the API server, and a Task is dispatched to a Message Queue. If a Task is present in the Queue, the Worker executes it. Static analysis utilizes Semgrep and Slither, while dynamic analysis operates on a Foundry-based system. Results from both types of analysis are interpreted, aggregated, and stored in Redis.

Users can access and review their analysis results using the Task ID associated with each request.

<figure><img src="../.gitbook/assets/master_page_m – PF - 3 (1).png" alt="" width="563"><figcaption></figcaption></figure>















