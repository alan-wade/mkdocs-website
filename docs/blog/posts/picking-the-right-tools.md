---
date:
    created: 2025-03-28
categories: 
    - Tooling
    - AI
---

# Picking the Right Tools

When starting a new project, it's important to choose the right tools. However, many people get so caught up in finding the perfect tool that they lose sight of what matters most: getting started.

<!-- more -->

The most important part of any new project is taking that first step. You could have access to the most sophisticated tools in the world, each perfectly optimized for specific scenarios. But none of that matters if you spend all your time searching through the toolbox instead of building. I've found that using simple, open-source tools for prototyping helps me learn faster and deliver more quickly than trying to find the perfect solution.

## My Prototyping Journey

### Tooling Overload

When I began exploring how to build a chatbot, I found myself overwhelmed by countless online resources. Zapier, n8n, Python tutorials, MCP – the options seemed endless. I was simply trying to validate my proof of concept and solidify my understanding of the project before diving in. That's when I discovered FlowiseAI. While this isn't meant to be an advertisement for open-source software, this tool proved incredibly valuable. I could use their templates as a starting point, experiment with different configurations, and understand how the connections would work with my actual tech stack.

### Playing with Flowise

The tool made it easy to access their marketplace, add a web scraper for their GitHub page, and start conversations with the built-in chatbot. Below you can see the configuration needed to initialize the bot.

---
<div style="text-align: center;">
    <img src="/blog/assets/flowiseai-example.png" alt="FlowiseAI Example" width="800px" style="border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
</div>
---

Now, I can hear you thinking, "Alan, after all that talk about not getting caught up in tool selection, it seems like you've done exactly that with FlowiseAI. Isn't that a bit hypocritical?"

It might appear that way, but this wasn't where my project ended. I used what I learned about integrations and web scraping from the tool to create my own Python implementation. The key insight was that while the no-code/low-code solution provided a helpful starting point, I could have achieved similar results with any of the platforms. Instead of getting stuck searching for the perfect starting point, I simply used the last tool I found, even though it wasn't ideal.

### Conclusion

When starting a project, stop obsessing over the latest tools or worrying about what some PhD on LinkedIn says about your current stack being outdated. Take action and build something. The sooner you create a baseline, the sooner you can iterate and see how your idea performs with real data and traffic.

To see how my chatbot experiments turned out, check out my portfolio case study or my [rag-experiments](https://github.com/alan-wade/rag-experiments) GitHub repository.


