---
layout: default
title: Best Practices
parent: Functions
nav_order: 9
---

# Functions Best Practices
{: .no_toc }

- TOC
{:toc}

### Performance and scaling
Organize function apps and functions for performance, scaling, 
and security. In an ASE multiple function apps can share the same 
resources. How the functions and function apps are grouped can impact the 
performance, scaling, configuration, deployment, and security.

### Optimize deployments
Keep in mind  all functions in a **function app** are deployed at the 
same time. Also, consider using deployment slots to minimize deployment 
downtime.

### Write functions to be stateless
Functions should be stateless and idempotent if possible. Associate any
required state information with your data.

### Write defensive functions
Design functions with the ability to continue from a previous fail point 
during the next execution.

### Use retry pattern
Use a retry pattern to handle transient failures. When a function fails 
to connect to a service or network resource, have it transparently retry 
the failed operation.

### Avoid long running functions
Large, long-running functions can cause unexpected timeout issues. 
Whenever possible, refactor large functions into smaller function sets that
work together and return responses fast.

### Avoid sharing storage accounts
Use a separate storage account for each function app to maximize 
performance.

### Use async code but avoid blocking calls
Asynchronous programming is a recommended best practice, especially when 
blocking I/O operations are involved.

### Add logic to protect data integrity
- Verify the existence of data before trying to execute a delete
- Check if data already exists before trying to execute a create action
- Reconciling logic that creates eventual consistency in data
- Concurrency controls
- Duplication controls
- Data freshness validation
- Guard logic to verify input data
