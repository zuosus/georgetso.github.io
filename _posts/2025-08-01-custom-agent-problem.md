---
title: "Navigating the Labyrinth of AI Agents and Custom Model Providers: My Last Two Days"
date: 2025-08-01
---

The past two days have been a deep dive into the fascinating, sometimes frustrating, world of AI agents and custom model providers. My goal was to find an agent that offers flexibility in choosing LLMs, particularly for cost-effective options like DeepSeek, and of course, leveraging the free tier of Gemini where possible. Here's a rundown of my adventures:

I started by experimenting with several AI agents, including Cline, Roo Code, and Claude Code. Each presented its own set of strengths and limitations. While some offered promising features, the real challenge lay in integrating custom model providers beyond the usual suspects.

My search eventually led me to claude-code-router, which seemed like a promising contender. It leverages the robust Claude Code agent as its foundation but offers the ability to configure custom model providers. This was a significant step in the right direction, as it opened up the possibility of using models not directly supported by the core Claude Code offering. However, I found the Model Context Protocol (MCP) configuration within claude-code-router to be less intuitive than I'd hoped. Getting it set up and working seamlessly with external models required a fair bit of tinkering.

I also had high hopes for Roo Code, particularly due to its open-source nature and reputation for being an autonomous coding assistant. Unfortunately, Roo Code currently only supports OpenAI-compatible custom providers, which limits the range of models that can be integrated. This was a deal-breaker for my primary goal of exploring more diverse and affordable LLMs.

Speaking of affordable, DeepSeek was at the top of my list. Its models are known for their very competitive pricing, making them an attractive option for frequent use. However, my experience trying to integrate DeepSeek as a model provider into the agents I explored didn't go as smoothly as I'd hoped. There were compatibility issues and a general lack of straightforward integration paths.

Naturally, I also wanted to leverage Gemini due to its free tier. While Gemini Flash is indeed free, I quickly discovered its limitations in terms of power and capability for more complex tasks. Opting for Gemini Pro, which offers greater performance, quickly racked up costs, leaving me almost a dollar poorer – a surprising hit for what I initially thought would be a free alternative!

In my quest for a truly flexible and cost-effective AI agent, I even submitted a Pull Request (PR) to block/goose, hoping to add support for DeepSeek as a model provider. Goose, an open-source agent developed by Block, looks like a really solid and extensible platform. Regrettably, my PR hasn't received any feedback yet, which is a bit disappointing as Goose, with DeepSeek integration, could be an excellent choice for many.

Overall, these past two days have been a valuable learning experience. The landscape of AI agents and custom model providers is rapidly evolving, and while there are powerful tools available, integrating diverse LLMs, especially those focused on affordability, still presents a challenge. The ideal solution would combine the robust capabilities of an agent like Goose or Claude Code with truly seamless and intuitive integration for a wide range of custom model providers. The search continues!
