---
title: "AI Agents and Custom Model Providers"
date: 2025-08-01
---

The past two days have been a deep dive into AI agents and custom model providers. My goal was to find an agent that offers flexibility in choosing LLMs, particularly for cost-effective options like DeepSeek, and leveraging the free tier of Gemini where possible. Here's a rundown:

I started by experimenting with several AI agents, including Cline, Roo Code, and Claude Code. Each presented its own set of strengths and limitations. While some offered promising features, the real challenge lay in integrating custom model providers beyond the usual suspects.

My search eventually led me to claude-code-router, which seemed like a promising contender. It leverages the robust Claude Code agent as its foundation but offers the ability to configure custom model providers. This was a good step, as it opened up the possibility of using models not directly supported by the core Claude Code offering. However, the Model Context Protocol (MCP) configuration within claude-code-router was not intuitive. Setting it up and working with external models required some work.

I also tried Roo Code, particularly due to its open-source nature and reputation for being an autonomous coding assistant. Unfortunately, Roo Code currently only supports OpenAI-compatible custom providers, which limits the range of models that can be integrated. This was not suitable for my primary goal of exploring more diverse and affordable LLMs.

Speaking of affordable, DeepSeek was at the top of my list. Its models are known for their very competitive pricing, making them an attractive option for frequent use. However, integrating DeepSeek as a model provider into the agents I explored was not smooth. There were compatibility issues and a general lack of straightforward integration paths.

I also wanted to use Gemini due to its free tier. While Gemini Flash is indeed free, I quickly discovered its limitations in terms of power and capability for more complex tasks. Opting for Gemini Pro, which offers greater performance, quickly racked up costs, leaving me almost a dollar poorer – a surprising cost for what I initially thought would be a free alternative!

In my quest for a flexible and cost-effective AI agent, I submitted a Pull Request (PR) to block/goose, to add support for DeepSeek as a model provider. Goose, an open-source agent developed by Block, looks like a solid and extensible platform. My PR hasn't received any feedback yet. Goose, with DeepSeek integration, could be an excellent choice for many.

Overall, these past two days have been a learning experience. The landscape of AI agents and custom model providers is rapidly evolving, and while there are powerful tools available, integrating diverse LLMs, especially those focused on affordability, still presents a challenge. The ideal solution would combine the robust capabilities of an agent like Goose or Claude Code with seamless and intuitive integration for a wide range of custom model providers.