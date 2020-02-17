---
title: SSE-LECTURE2-TRUESEC
date: 2019-01-30 09:19:10
tags:
- Secure Software Engineering
categories: 学习
---

### Validation
- **always** prefer white listing, before black listing
- **always** prefer strict validation
- normaliztion and sanitation is for edge cases only!

### Untrusted Pattern
- highlight the trust boundary
- less intrusive to existing code

### Implementation - Immutability
- Drastically reduce the risk of TOCTTOU problems
- Increases readability
- Increases parallelism
- Increases event sourcing

### Implementation - Pessimistic Strategy


### Implementation - Isolate risks
- compartmentalize sensitive operations
- Risk separation: Parsing of certain formats(XML), consider external dependencies
- Security testing