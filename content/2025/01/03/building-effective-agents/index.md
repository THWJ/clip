---
title: "构建有效代理人\人择"
date: 2025-01-03T11:24:53+08:00
updated: 2025-01-03T11:24:53+08:00
taxonomies:
  tags: []
extra:
  source: https://www.anthropic.com/research/building-effective-agents
  hostname: www.anthropic.com
  author: 
  original_title: "Building effective agents"
  original_lang: en
---

Over the past year, we've worked with dozens of teams building large language model (LLM) agents across industries. Consistently, the most successful implementations weren't using complex frameworks or specialized libraries. Instead, they were building with simple, composable patterns.  

在过去的一年里，我们与数十个团队合作，构建跨行业的大型语言模型（LLM）代理。同样，最成功的实现并没有使用复杂的框架或专门的库。相反，他们用简单的、可组合的模式进行构建。

In this post, we share what we’ve learned from working with our customers and building agents ourselves, and give practical advice for developers on building effective agents.  

在这篇文章中，我们分享了我们从与客户和建筑代理合作中学到的东西，并为开发人员提供了关于构建有效代理的实用建议。

## What are agents?  什么是代理人？

"Agent" can be defined in several ways. Some customers define agents as fully autonomous systems that operate independently over extended periods, using various tools to accomplish complex tasks. Others use the term to describe more prescriptive implementations that follow predefined workflows. At Anthropic, we categorize all these variations as **agentic systems**, but draw an important architectural distinction between **workflows** and **agents**:  

“代理人”可以用几种方式定义。一些客户将代理定义为完全自主的系统，这些系统在很长一段时间内独立运行，使用各种工具来完成复杂的任务。其他人则使用该术语来描述遵循预定义工作流的更具规范性的实现。在Anthropic，我们将所有这些变体归类为**代理系统**，但在**工作流**和**代理**之间绘制了一个重要的架构区别：

-   **Workflows** are systems where LLMs and tools are orchestrated through predefined code paths.  
    
    **工作流**是LLMs和工具通过预定义的代码路径编排的系统。
-   **Agents**, on the other hand, are systems where LLMs dynamically direct their own processes and tool usage, maintaining control over how they accomplish tasks.  
    
    另一方面，**代理**是LLMs动态指导自己的流程和工具使用的系统，保持对他们如何完成任务的控制。

Below, we will explore both types of agentic systems in detail. In Appendix 1 (“Agents in Practice”), we describe two domains where customers have found particular value in using these kinds of systems.  

下面，我们将详细探讨这两种类型的代理系统。在附录1（“实践中的代理”）中，我们描述了两个领域，客户发现使用这些类型的系统具有特殊价值。

## When (and when not) to use agents  

何时（以及何时不）使用代理

When building applications with LLMs, we recommend finding the simplest solution possible, and only increasing complexity when needed. This might mean not building agentic systems at all. Agentic systems often trade latency and cost for better task performance, and you should consider when this tradeoff makes sense.  

在使用LLMs构建应用程序时，我们建议找到最简单的解决方案，只在需要时增加复杂性。这可能意味着根本不建立代理系统。智能系统经常以延迟和成本换取更好的任务性能，您应该考虑这种权衡何时有意义。

When more complexity is warranted, workflows offer predictability and consistency for well-defined tasks, whereas agents are the better option when flexibility and model-driven decision-making are needed at scale. For many applications, however, optimizing single LLM calls with retrieval and in-context examples is usually enough.  

当需要更多的复杂性时，工作流为定义明确的任务提供了可预测性和一致性，而当需要大规模的灵活性和模型驱动的决策时，代理是更好的选择。然而，对于许多应用程序，使用检索和上下文示例优化单个LLM调用通常就足够了。

## When and how to use frameworks  

何时以及如何使用框架

There are many frameworks that make agentic systems easier to implement, including:  

有许多框架可以使代理系统更容易实现，包括：

-   [LangGraph](https://langchain-ai.github.io/langgraph/) from LangChain;  
    
    LangChain中的[LangGraph](https://langchain-ai.github.io/langgraph/);
-   Amazon Bedrock's [AI Agent framework](https://aws.amazon.com/bedrock/agents/);  
    
    Amazon Bedrock的[AI Agent框架](https://aws.amazon.com/bedrock/agents/);
-   [Rivet](https://rivet.ironcladapp.com/), a drag and drop GUI LLM workflow builder; and  
    
    [铆钉](https://rivet.ironcladapp.com/)，拖放GUILLM工作流构建器;以及
-   [Vellum](https://www.vellum.ai/), another GUI tool for building and testing complex workflows.  
    
    [Vellum](https://www.vellum.ai/)是另一个用于构建和测试复杂工作流的GUI工具。

These frameworks make it easy to get started by simplifying standard low-level tasks like calling LLMs, defining and parsing tools, and chaining calls together. However, they often create extra layers of abstraction that can obscure the underlying prompts and responses, making them harder to debug. They can also make it tempting to add complexity when a simpler setup would suffice.  

这些框架简化了标准的低级任务，如调用LLMs、定义和解析工具以及将调用链接在一起，从而使入门变得容易。但是，它们通常会创建额外的抽象层，从而可能会掩盖底层提示 和响应，使它们更难调试。当一个简单的设置就足够了的时候，它们也会让你增加复杂性。

We suggest that developers start by using LLM APIs directly: many patterns can be implemented in a few lines of code. If you do use a framework, ensure you understand the underlying code. Incorrect assumptions about what's under the hood are a common source of customer error.  

我们建议开发人员从直接使用LLMAPI开始：许多模式可以在几行代码中实现。如果你使用框架，确保你理解底层代码。对引擎盖下的内容的错误假设是客户错误的常见来源。

See our [cookbook](https://github.com/anthropics/anthropic-cookbook/tree/main/patterns/agents) for some sample implementations.  

请参阅我们[的cookbook](https://github.com/anthropics/anthropic-cookbook/tree/main/patterns/agents)以获取一些示例实现。

## Building blocks, workflows, and agents  

构建块、工作流程和代理

In this section, we’ll explore the common patterns for agentic systems we’ve seen in production. We'll start with our foundational building block—the augmented LLM—and progressively increase complexity, from simple compositional workflows to autonomous agents.  

在本节中，我们将探讨我们在生产中看到的代理系统的常见模式。我们将从我们的基础构建块-增强的LLM-开始，并逐步增加复杂性，从简单的组合工作流到自治代理。

### Building block: The augmented LLM  

构建模块：增强的LLM

The basic building block of agentic systems is an LLM enhanced with augmentations such as retrieval, tools, and memory. Our current models can actively use these capabilities—generating their own search queries, selecting appropriate tools, and determining what information to retain.  

![the augented LLM](<the_augmented_LLM.png>)

代理系统的基本构建块是一个LLM增强与扩增，如检索，工具和内存。我们目前的模型可以积极地使用这些功能生成自己的搜索查询，选择适当的工具，并确定要保留哪些信息。

We recommend focusing on two key aspects of the implementation: tailoring these capabilities to your specific use case and ensuring they provide an easy, well-documented interface for your LLM. While there are many ways to implement these augmentations, one approach is through our recently released [Model Context Protocol](https://www.anthropic.com/news/model-context-protocol), which allows developers to integrate with a growing ecosystem of third-party tools with a simple [client implementation](https://modelcontextprotocol.io/tutorials/building-a-client#building-mcp-clients).  

我们建议关注实现的两个关键方面：根据您的特定用例定制这些功能，并确保它们为您LLM提供简单，文档齐全的界面。虽然有很多方法可以实现这些增强，但其中一种方法是通过我们最近发布[的模型上下文协议](https://www.anthropic.com/news/model-context-protocol)，该协议允许开发人员通过简单[的客户端实现](https://modelcontextprotocol.io/tutorials/building-a-client#building-mcp-clients)与不断增长的第三方工具生态系统集成。

For the remainder of this post, we'll assume each LLM call has access to these augmented capabilities.  

在本文的其余部分，我们将假设每个LLM调用都可以访问这些增强的功能。

### Workflow: Prompt chaining  

工作流：提示链接

Prompt chaining decomposes a task into a sequence of steps, where each LLM call processes the output of the previous one. You can add programmatic checks (see "gate” in the diagram below) on any intermediate steps to ensure that the process is still on track.  

![alt text](<the_prompt_chaining_workflow.webp>)

提示链接将任务分解为一系列步骤，其中每个LLM调用处理前一个的输出。您可以在任何中间步骤上添加程序化检查（请参见下图中的“gate”），以确保流程仍在正常运行。

**When to use this workflow:** This workflow is ideal for situations where the task can be easily and cleanly decomposed into fixed subtasks. The main goal is to trade off latency for higher accuracy, by making each LLM call an easier task.  

**何时使用此工作流：**此工作流适用于任务可以轻松干净地分解为固定子任务的情况。主要目标是通过使每个LLM调用更容易来权衡延迟以获得更高的准确性。

**Examples where prompt chaining is useful:  

提示链接有用的示例：**

-   Generating Marketing copy, then translating it into a different language.  
    
    生成营销文案，然后将其翻译成不同的语言。
-   Writing an outline of a document, checking that the outline meets certain criteria, then writing the document based on the outline.  
    
    编写文档的大纲，检查大纲是否符合某些标准，然后根据大纲编写文档。

### Workflow: Routing  工作流程：工艺路线

Routing classifies an input and directs it to a specialized followup task. This workflow allows for separation of concerns, and building more specialized prompts. Without this workflow, optimizing for one kind of input can hurt performance on other inputs.  
![alt text](<the_routing_workflow.webp>)
路由对输入进行分类并将其引导到专门的后续任务。此工作流允许分离关注点，并构建更专业的提示。如果没有此工作流，针对一种输入进行优化可能会损害其他输入的性能。

**When to use this workflow:** Routing works well for complex tasks where there are distinct categories that are better handled separately, and where classification can be handled accurately, either by an LLM or a more traditional classification model/algorithm.  

**何时使用此工作流：**路由适用于复杂的任务，其中有不同的类别，可以更好地单独处理，并且可以通过LLM或更传统的分类模型/算法准确处理分类。LLM

**Examples where routing is useful:  

路由有用的示例：**

-   Directing different types of customer service queries (general questions, refund requests, technical support) into different downstream processes, prompts, and tools.  
    
    将不同类型的客户服务查询（一般问题，退款请求，技术支持）导入不同的下游流程，提示和工具。
-   Routing easy/common questions to smaller models like Claude 3.5 Haiku and hard/unusual questions to more capable models like Claude 3.5 Sonnet to optimize cost and speed.  
    
    将简单/常见的问题路由到较小的模型（如Claude 3.5 Haiku），将困难/不寻常的问题路由到功能更强大的模型（如Claude 3.5 Sonnet），以优化成本和速度。

### Workflow: Parallelization  

工作流程：凝胶化

LLMs can sometimes work simultaneously on a task and have their outputs aggregated programmatically. This workflow, parallelization, manifests in two key variations:  

LLMs有时可以同时处理一个任务，并以编程方式聚合其输出。这种工作流（并行化）表现为两个关键变化：

-   **Sectioning**: Breaking a task into independent subtasks run in parallel.  
    
    **分段**：将一个任务分解为并行运行的独立子任务。
-   **Voting:** Running the same task multiple times to get diverse outputs.  
    
    **投票：**多次运行相同的任务以获得不同的输出。
![alt text](<the_parallelization_workflow.webp>)
**When to use this workflow:** Parallelization is effective when the divided subtasks can be parallelized for speed, or when multiple perspectives or attempts are needed for higher confidence results. For complex tasks with multiple considerations, LLMs generally perform better when each consideration is handled by a separate LLM call, allowing focused attention on each specific aspect.  

**何时使用此工作流：**当划分的子任务可以并行化以提高速度时，或者当需要多个视角或尝试以获得更高置信度的结果时，并行化是有效的。对于具有多个考虑因素的复杂任务，当每个考虑因素由单独的LLM调用处理时LLMs通常会执行得更好，从而可以将注意力集中在每个特定方面。

**Examples where parallelization is useful:  

并行化有用的示例：**

-   **Sectioning**:  
    
    **切片**：
    -   Implementing guardrails where one model instance processes user queries while another screens them for inappropriate content or requests. This tends to perform better than having the same LLM call handle both guardrails and the core response.  
        
        实现护栏，其中一个模型实例处理用户查询，而另一个模型实例筛选不适当的内容或请求。这往往比让同一个LLM调用同时处理guarrails和核心响应的性能更好。
    -   Automating evals for evaluating LLM performance, where each LLM call evaluates a different aspect of the model’s performance on a given prompt.  
        
        自动评估LLM性能，其中每个LLM调用在给定提示符上评估模型性能的不同方面。
-   **Voting**:  
    
    **表决**：
    -   Reviewing a piece of code for vulnerabilities, where several different prompts review and flag the code if they find a problem.  
        
        检查一段代码是否存在漏洞，如果发现问题，会有几个不同的提示检查并标记代码。
    -   Evaluating whether a given piece of content is inappropriate, with multiple prompts evaluating different aspects or requiring different vote thresholds to balance false positives and negatives.  
        
        评估给定的内容是否不合适，多个提示评估不同的方面或要求不同的投票阈值来平衡误报和漏报。

### Workflow: Orchestrator-workers  

工作流程：工作人员

In the orchestrator-workers workflow, a central LLM dynamically breaks down tasks, delegates them to worker LLMs, and synthesizes their results.  
![alt text](<the_orchestrator-workers_workflow.webp>)
在协调器-工作者工作流中，中央LLM动态地分解任务，将它们委托给工作者LLMs，并合成它们的结果。

**When to use this workflow:** This workflow is well-suited for complex tasks where you can’t predict the subtasks needed (in coding, for example, the number of files that need to be changed and the nature of the change in each file likely depend on the task). Whereas it’s topographically similar, the key difference from parallelization is its flexibility—subtasks aren't pre-defined, but determined by the orchestrator based on the specific input.  

**何时使用此工作流：**此工作流非常适合无法预测所需子任务的复杂任务（例如，在编码中，需要更改的文件数量以及每个文件中更改的性质可能取决于任务）。尽管它在拓扑上很相似，但与并行化的关键区别在于它的灵活性子任务不是预定义的，而是由编排器根据特定的输入来确定的。

**Example where orchestrator-workers is useful:  

orchestator-workers有用的示例：**

-   Coding products that make complex changes to multiple files each time.  
    
    每次对多个文件进行复杂更改的编码产品。
-   Search tasks that involve gathering and analyzing information from multiple sources for possible relevant information.  
    
    搜索任务涉及从多个来源收集和分析信息，以获得可能的相关信息。

### Workflow: Evaluator-optimizer  

工作流程：评估器-优化器

In the evaluator-optimizer workflow, one LLM call generates a response while another provides evaluation and feedback in a loop.  
![alt text](<the_evaluator-optimizer_workflow.webp>)
在评估器-优化器工作流中，一个LLM调用生成响应，而另一个调用在循环中提供评估和反馈。

**When to use this workflow:** This workflow is particularly effective when we have clear evaluation criteria, and when iterative refinement provides measurable value. The two signs of good fit are, first, that LLM responses can be demonstrably improved when a human articulates their feedback; and second, that the LLM can provide such feedback. This is analogous to the iterative writing process a human writer might go through when producing a polished document.  

**何时使用此工作流：**当我们有明确的评估标准，并且迭代细化提供可衡量的价值时，此工作流特别有效。良好拟合的两个标志是，第一，当人类表达他们的反馈时LLM响应可以明显改善;第二，LLM可以提供这样的反馈。这类似于一个人类作家在制作一个精美的文档时可能经历的迭代写作过程。

**Examples where evaluator-optimizer is useful:  

evaluator-optimizer有用的例子：**

-   Literary translation where there are nuances that the translator LLM might not capture initially, but where an evaluator LLM can provide useful critiques.  
    
    文学翻译，其中有细微差别，译者LLM可能不会捕获最初，但其中评估LLM可以提供有用的批评。
-   Complex search tasks that require multiple rounds of searching and analysis to gather comprehensive information, where the evaluator decides whether further searches are warranted.  
    
    复杂的搜索任务，需要多轮搜索和分析，以收集全面的信息，评估人员决定是否需要进一步搜索。

### Agents  剂

Agents are emerging in production as LLMs mature in key capabilities—understanding complex inputs, engaging in reasoning and planning, using tools reliably, and recovering from errors. Agents begin their work with either a command from, or interactive discussion with, the human user. Once the task is clear, agents plan and operate independently, potentially returning to the human for further information or judgement. During execution, it's crucial for the agents to gain “ground truth” from the environment at each step (such as tool call results or code execution) to assess its progress. Agents can then pause for human feedback at checkpoints or when encountering blockers. The task often terminates upon completion, but it’s also common to include stopping conditions (such as a maximum number of iterations) to maintain control.  

随着LLMs在关键能力方面的成熟，Agent正在生产中出现-理解复杂的输入，参与推理和规划，可靠地使用工具，并从错误中恢复。代理开始他们的工作，从一个命令，或交互式讨论，人类用户。一旦任务明确，智能体就独立地计划和操作，可能会返回人类以获得进一步的信息或判断。在执行过程中，对于代理来说，在每个步骤（例如工具调用结果或代码执行）从环境中获得“地面实况”以评估其进度至关重要。然后，代理可以在检查点或遇到拦截器时暂停人工反馈。任务通常在完成时终止，但通常也包括停止条件（例如最大迭代次数）以保持控制。

Agents can handle sophisticated tasks, but their implementation is often straightforward. They are typically just LLMs using tools based on environmental feedback in a loop. It is therefore crucial to design toolsets and their documentation clearly and thoughtfully. We expand on best practices for tool development in Appendix 2 ("Prompt Engineering your Tools").  

代理可以处理复杂的任务，但它们的实现通常很简单。它们通常只是LLMs使用基于循环中的环境反馈的工具。因此，清晰而周到地设计工具集及其文档至关重要。我们在附录2（“立即设计您的工具”）中扩展了工具开发的最佳实践。
![alt text](<autonomous_agent.png>)
**When to use agents:** Agents can be used for open-ended problems where it’s difficult or impossible to predict the required number of steps, and where you can’t hardcode a fixed path. The LLM will potentially operate for many turns, and you must have some level of trust in its decision-making. Agents' autonomy makes them ideal for scaling tasks in trusted environments.  

**何时使用代理：**代理可以用于开放式问题，在这些问题中，很难或不可能预测所需的步骤数，并且您无法硬编码固定路径。LLM可能会运行许多回合，您必须对其决策有一定程度的信任。代理的自主性使其成为可信环境中扩展任务的理想选择。

The autonomous nature of agents means higher costs, and the potential for compounding errors. We recommend extensive testing in sandboxed environments, along with the appropriate guardrails.  

代理人的自主性意味着更高的成本，以及复合错误的可能性。我们建议在沙盒环境中进行广泛的测试，沿着适当的护栏。

**Examples where agents are useful:  

试剂有用的示例：**

The following examples are from our own implementations:  

下面的例子来自我们自己的实现：

-   A coding Agent to resolve [SWE-bench tasks](https://www.anthropic.com/research/swe-bench-sonnet), which involve edits to many files based on a task description;  
    
    一个编码代理来解决[SWE工作台任务](https://www.anthropic.com/research/swe-bench-sonnet)，这涉及到基于任务描述的许多文件的编辑;
-   Our [“computer use” reference implementation](https://github.com/anthropics/anthropic-quickstarts/tree/main/computer-use-demo), where Claude uses a computer to accomplish tasks.  
    
    我们的[“计算机使用”参考实现](https://github.com/anthropics/anthropic-quickstarts/tree/main/computer-use-demo)，其中克劳德使用计算机来完成任务。
![alt text](<High-level_flow_of_a_coding_agent.webp>)
## Combining and customizing these patterns  

组合和定制这些模式

These building blocks aren't prescriptive. They're common patterns that developers can shape and combine to fit different use cases. The key to success, as with any LLM features, is measuring performance and iterating on implementations. To repeat: you should consider adding complexity _only_ when it demonstrably improves outcomes.  

这些构建模块不是规定性的。它们是开发人员可以塑造和联合收割机以适应不同用例的常见模式。与任何LLM特性一样，成功的关键是测量性能和迭代实现。重复一遍：_只有_当它明显改善结果时，你才应该考虑增加复杂性。

## Summary  总结

Success in the LLM space isn't about building the most sophisticated system. It's about building the _right_ system for your needs. Start with simple prompts, optimize them with comprehensive evaluation, and add multi-step agentic systems only when simpler solutions fall short.  

LLM领域的成功并不在于构建最复杂的系统。它是关于根据您的需求构建_正确_的系统。从简单的提示开始，通过全面的评估来优化它们，只有当简单的解决方案不足时才添加多步代理系统。

When implementing agents, we try to follow three core principles:  

在执行代理时，我们试图遵循三个核心原则：

1.  Maintain **simplicity** in your agent's design.  
    
    保持代理设计的**简单性**。
2.  Prioritize **transparency** by explicitly showing the agent’s planning steps.  
    
    通过明确显示代理的规划步骤来优先考虑**透明度**。
3.  Carefully craft your agent-computer interface (ACI) through thorough tool **documentation and testing**.  
    
    通过全面的工具**文档和测试，**精心制作代理-计算机接口（ACI）。

Frameworks can help you get started quickly, but don't hesitate to reduce abstraction layers and build with basic components as you move to production. By following these principles, you can create agents that are not only powerful but also reliable, maintainable, and trusted by their users.  

框架可以帮助您快速入门，但在您转向生产环境时，请不要犹豫，减少抽象层并使用基本组件进行构建。通过遵循这些原则，您可以创建不仅功能强大，而且可靠，可维护且受用户信任的代理。

### Acknowledgements  确认

Written by Erik Schluntz and Barry Zhang. This work draws upon our experiences building agents at Anthropic and the valuable insights shared by our customers, for which we're deeply grateful.  

编剧：Erik Schluntz和巴里张。这项工作借鉴了我们在Anthropic构建代理的经验以及我们客户分享的宝贵见解，对此我们深表感谢。

## Appendix 1: Agents in practice  

附录1：实践中的代理

Our work with customers has revealed two particularly promising applications for AI agents that demonstrate the practical value of the patterns discussed above. Both applications illustrate how agents add the most value for tasks that require both conversation and action, have clear success criteria, enable feedback loops, and integrate meaningful human oversight.  

我们与客户的合作揭示了AI代理的两个特别有前途的应用，证明了上面讨论的模式的实用价值。这两个应用程序都说明了智能体如何为需要对话和行动的任务增加最大价值，具有明确的成功标准，实现反馈循环，并集成有意义的人类监督。

### A. Customer support  A.客户支持

Customer support combines familiar chatbot interfaces with enhanced capabilities through tool integration. This is a natural fit for more open-ended agents because:  

客户支持通过工具集成将熟悉的聊天机器人界面与增强的功能相结合。这自然适合更开放的代理人，因为：

-   Support interactions naturally follow a conversation flow while requiring access to external information and actions;  
    
    支持交互自然遵循对话流程，同时需要访问外部信息和操作;
-   Tools can be integrated to pull customer data, order history, and knowledge base articles;  
    
    可以集成工具来提取客户数据、订单历史记录和知识库文章;
-   Actions such as issuing refunds or updating tickets can be handled programmatically; and  
    
    可以通过编程方式处理退款或更新机票等操作;以及
-   Success can be clearly measured through user-defined resolutions.  
    
    成功可以通过用户定义的分辨率来明确衡量。

Several companies have demonstrated the viability of this approach through usage-based pricing models that charge only for successful resolutions, showing confidence in their agents' effectiveness.  

几家公司已经通过基于使用的定价模式证明了这种方法的可行性，这种模式只对成功的解决方案收费，显示出对代理人效率的信心。

### B. Coding agents  B。编码剂

The software development space has shown remarkable potential for LLM features, with capabilities evolving from code completion to autonomous problem-solving. Agents are particularly effective because:  

软件开发领域已经显示出LLM功能的巨大潜力，其功能从代码完成发展到自主解决问题。代理商特别有效，因为：

-   Code solutions are verifiable through automated tests;  
    
    代码解决方案可通过自动化测试进行验证;
-   Agents can iterate on solutions using test results as feedback;  
    
    代理可以使用测试结果作为反馈来验证解决方案;
-   The problem space is well-defined and structured; and  
    
    问题空间定义明确，结构合理;
-   Output quality can be measured objectively.  
    
    输出质量可以客观地衡量。

In our own implementation, agents can now solve real GitHub issues in the [SWE-bench Verified](https://www.anthropic.com/research/swe-bench-sonnet) benchmark based on the pull request description alone. However, whereas automated testing helps verify functionality, human review remains crucial for ensuring solutions align with broader system requirements.  

在我们自己的实现中，代理现在可以单独基于拉取请求描述在[SWE-bench Verified](https://www.anthropic.com/research/swe-bench-sonnet)基准中解决真实的GitHub问题。然而，尽管自动化测试有助于验证功能，但人工审查对于确保解决方案符合更广泛的系统需求仍然至关重要。

## Appendix 2: Prompt engineering your tools  

附录2：快速设计您的工具

No matter which agentic system you're building, tools will likely be an important part of your agent. [Tools](https://www.anthropic.com/news/tool-use-ga) enable Claude to interact with external services and APIs by specifying their exact structure and definition in our API. When Claude responds, it will include a [tool use block](https://docs.anthropic.com/en/docs/build-with-claude/tool-use#example-api-response-with-a-tool-use-content-block) in the API response if it plans to invoke a tool. Tool definitions and specifications should be given just as much prompt engineering attention as your overall prompts. In this brief appendix, we describe how to prompt engineer your tools.  

无论你正在构建哪种代理系统，工具都可能是你的代理的重要组成部分。[工具](https://www.anthropic.com/news/tool-use-ga)使Claude能够通过在我们的API中指定外部服务和API的确切结构和定义来与它们进行交互。当Claude响应时，如果它计划调用工具，它将在API响应中包括[工具使用块](https://docs.anthropic.com/en/docs/build-with-claude/tool-use#example-api-response-with-a-tool-use-content-block)。工具定义和规格应给予尽可能多的提示工程的注意，因为你的整体提示。在这个简短的附录中，我们描述了如何提示工程师您的工具。

There are often several ways to specify the same action. For instance, you can specify a file edit by writing a diff, or by rewriting the entire file. For structured output, you can return code inside markdown or inside JSON. In software engineering, differences like these are cosmetic and can be converted losslessly from one to the other. However, some formats are much more difficult for an LLM to write than others. Writing a diff requires knowing how many lines are changing in the chunk header before the new code is written. Writing code inside JSON (compared to markdown) requires extra escaping of newlines and quotes.  

通常有几种方法来指定同一个动作。例如，您可以通过编写diff或重写整个文件来指定文件编辑。对于结构化输出，您可以在markdown或JSON中返回代码。在软件工程中，像这样的差异是装饰性的，可以从一个转换到另一个。然而，有些格式对于LLM来说比其他格式更难编写。LLM编写diff需要在编写新代码之前知道chunk header中有多少行发生了变化。在JSON中编写代码（与markdown相比）需要对换行符和引号进行额外的转义。

Our suggestions for deciding on tool formats are the following:  

我们对决定工具格式的建议如下：

-   Give the model enough tokens to "think" before it writes itself into a corner.  
    
    在模型陷入困境之前，给它足够的令牌来“思考”。
-   Keep the format close to what the model has seen naturally occurring in text on the internet.  
    
    保持格式接近模型在互联网上自然出现的文本。
-   Make sure there's no formatting "overhead" such as having to keep an accurate count of thousands of lines of code, or string-escaping any code it writes.  
    
    确保没有格式化的“开销”，比如必须准确地计算数千行代码，或者对它编写的任何代码进行字符串转义。

One rule of thumb is to think about how much effort goes into human-computer interfaces (HCI), and plan to invest just as much effort in creating good _agent_\-computer interfaces (ACI). Here are some thoughts on how to do so:  

一个经验法则是考虑在人机接口（HCI）上投入了多少精力，并计划在创建良好_的代理_\-计算机接口（ACI）上投入同样多的精力。以下是关于如何做到这一点的一些想法：

-   Put yourself in the model's shoes. Is it obvious how to use this tool, based on the description and parameters, or would you need to think carefully about it? If so, then it’s probably also true for the model. A good tool definition often includes example usage, edge cases, input format requirements, and clear boundaries from other tools.  
    
    站在模特的角度想想。根据描述和参数，如何使用这个工具是显而易见的，还是需要仔细考虑？如果是这样的话，那么它可能也适用于模型。一个好的工具定义通常包括示例用法、边缘情况、输入格式要求以及与其他工具的明确界限。
-   How can you change parameter names or descriptions to make things more obvious? Think of this as writing a great docstring for a junior developer on your team. This is especially important when using many similar tools.  
    
    如何更改参数名称或描述以使事情更明显？可以把这看作是为团队中的初级开发人员编写一个很棒的文档字符串。在使用许多类似工具时，这一点尤其重要。
-   Test how the model uses your tools: Run many example inputs in our [workbench](https://console.anthropic.com/workbench) to see what mistakes the model makes, and iterate.  
    
    测试模型如何使用您的工具：在我们[的工作台](https://console.anthropic.com/workbench)中运行许多示例输入，以查看模型会犯哪些错误，然后进行验证。
-   [Poka-yoke](https://en.wikipedia.org/wiki/Poka-yoke) your tools. Change the arguments so that it is harder to make mistakes.  
    
    [把](https://en.wikipedia.org/wiki/Poka-yoke)你的工具都锁起来改变论点，这样就更难犯错误。

While building our agent for [SWE-bench](https://www.anthropic.com/research/swe-bench-sonnet), we actually spent more time optimizing our tools than the overall prompt. For example, we found that the model would make mistakes with tools using relative filepaths after the agent had moved out of the root directory. To fix this, we changed the tool to always require absolute filepaths—and we found that the model used this method flawlessly.  

在为[SWE-bench](https://www.anthropic.com/research/swe-bench-sonnet)构建代理时，我们实际上花了比整体提示更多的时间来优化工具。例如，我们发现，在代理移出根目录之后，使用相对文件路径的工具会使模型出错。为了解决这个问题，我们将工具更改为始终需要绝对文件路径-我们发现模型可以轻松地使用此方法。
