---
title: "Serverless: From Theory to Practice"
date: 2025-07-26
---

Several years ago, when AWS first introduced its serverless offerings, an article described how serverless functions enabled cloud providers like AWS to achieve unprecedented hardware utilization efficiency while allowing developers to completely offload scalability concerns to the platform. The idea of not having to predict traffic patterns or manually configure scaling rules was appealing.

### The Hesitation Period

Despite this vision, I had not worked with serverless functions in my professional projects. Traditional architectures with dedicated servers and manual scaling remained my daily reality. Serverless seemed like a concept for "other people's projects".

### Discovering Cloudflare Workers

This changed recently when budget constraints led me to explore Cloudflare Workers for hosting my personal website. Through research, I realized: **serverless functions aren't what I initially imagined**. 

They're not the simple, single-purpose pure functions I regularly write in my day job (typically just 10-20 lines of focused logic). Instead, serverless functions represent powerful, composable units of capability:

- My **API Worker** handles database connections, caching, user authentication, and even serves as a gateway for GenAI LLM outputs
- My **Web Worker** leverages Next.js SSG (Static Site Generation) to deliver performant web pages

### The Serverless Experience

Now that I'm using serverless architecture, I can confirm that those early articles were right. The ability to completely delegate scalability to the platform - whether it's AWS, GCP, or Cloudflare - is a big change. 

Some key benefits I've observed:
1. **Zero scaling operations**: Traffic spikes are handled automatically
2. **Reduced cognitive load**: I spend more time on business logic than infrastructure
3. **Cost efficiency**: Pay-per-use model aligns perfectly with my budget constraints

This architecture has fundamentally changed how I think about deploying web applications. What began as a budget-conscious decision has turned into an architectural preference. Serverless delivers on its promises of simplicity and scalability.