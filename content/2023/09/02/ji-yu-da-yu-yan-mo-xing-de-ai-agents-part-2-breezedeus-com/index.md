---
title: 基于大语言模型的AI Agents—Part 2
date: 2023-09-02T01:15:10.000Z
updated: 2023-09-02T01:15:10.000Z
taxonomies:
  tags:
    - Tech
extra:
  source: https://www.breezedeus.com/article/ai-agent-part2
  hostname: www.breezedeus.com
  author: null
  original_title: 基于大语言模型的AI Agents—Part 2 | Breezedeus.com
  original_lang: und

---

![notion image](x4OGw5R.jpg)

**本系列分享 Part 1:**

## [](https://www.breezedeus.com/article/ai-agent-part2#408297e5cac6465db000f1fbc49e3067 "AI Agent 回顾")AI Agent 回顾

**代理（Agent）**指能自主感知环境并采取行动实现目标的**智能体**。基于大语言模型（LLM）的 AI Agent 利用 LLM 进行记忆检索、决策推理和行动顺序选择等，把Agent的智能程度提升到了新的高度。LLM驱动的Agent具体是怎么做的呢？接下来的系列分享会介绍 AI Agent 当前最新的技术进展。

![notion image](https3A2F2Fs3-us-west-2.amazonaws.com2Fsecure.notion-static.com2Fdd719d9b-7bb4-44f3-a9cf-8a147aeaa3462FUntitled.png)

一个精简的Agent决策流程：

**Agent：P（感知）→ P（规划）→ A（行动）**

**感知（Perception）**是指Agent从环境中收集信息并从中提取相关知识的能力。

**规划（Planning）**是指Agent为了某一目标而作出的决策过程。

**行动（Action）**是指基于环境和规划做出的动作。

其中，**Policy**是Agent做出Action的核心决策，而行动又通过**观察（Observation）**成为进一步Perception的前提和基础，形成自主地闭环学习过程。

接下来介绍3个热门的Agent框架：**AutoGPT**、**GPT-Engineer** 和 **MetaGPT**。

## [](https://www.breezedeus.com/article/ai-agent-part2#72558ba58e6a419dac4f3d484f60bde7 "AutoGPT")AutoGPT

-   [](https://github.com/Significant-Gravitas/Auto-GPT)

-   Ref: [LLM Powered Autonomous Agents | Lil'Log](https://lilianweng.github.io/posts/2023-06-23-agent/)

**[AutoGPT](https://github.com/Significant-Gravitas/Auto-GPT)** 定位类似个人助理，帮助用户完成指定的任务，如调研某个课题。AutoGPT比较强调对外部工具的使用，如搜索引擎、页面浏览等。

以下是 AutoGPT 使用的 system prompt，其中 `{{...}}` 为用户输入:

## [](https://www.breezedeus.com/article/ai-agent-part2#0b3169ae0912440ab3c5d3b224605f46 "GPT-Engineer")[GPT-Engineer](https://github.com/AntonOsika/gpt-engineer)

-   Ref: [LLM Powered Autonomous Agents | Lil'Log](https://lilianweng.github.io/posts/2023-06-23-agent/)

[GPT-Engineer](https://github.com/AntonOsika/gpt-engineer) 旨在根据自然语言中指定的任务**创建一个完整的代码仓库**。GPT-Engineer 被指导去构建的一系列较小的组件，并在需要时**要求用户输入以澄清问题**。

以下是GPT-Engineer的一个任务澄清的样例对话。用户的输入在 `{{user input text}}`中。

在澄清之后，Agent 进入了**代码编写**模式。看官方视频，所有文件的内容是一次性生成的。System message:

对话样例:

## [](https://www.breezedeus.com/article/ai-agent-part2#f76b5a41c92c4bbcb396733a1b508001 "MetaGPT")MetaGPT

-   [](https://github.com/geekan/MetaGPT)

-   作者介绍视频：[https://www.bilibili.com/video/BV1Ru411V7XL](https://www.bilibili.com/video/BV1Ru411V7XL)

MetaGPT 现在可以生成2000行左右代码的项目，未来目标是万行甚至更长。

### [](https://www.breezedeus.com/article/ai-agent-part2#1a659a3e7254485ca305d1efe26f5cb9 "结构")结构

-   **Roles**

-   **Actions**

-   Environment

-   **Memory**

-   **Tools**

-   LLM Providers

![notion image](https3A2F2Fs3-us-west-2.amazonaws.com2Fsecure.notion-static.com2F7e3a0fda-d79e-4fa7-957e-19ce163abdc72FUntitled.png)

### [](https://www.breezedeus.com/article/ai-agent-part2#cb711b49b1fb4008a14c419bcf782913 "Multi-Agents 软件公司")Multi-Agents 软件公司

![notion image](https3A2F2Fs3-us-west-2.amazonaws.com2Fsecure.notion-static.com2F6322cfd0-8da5-456e-a127-98cd9ca1c0d32FUntitled.png)

创建公司和雇员：

实现时，循环依次调用各个角色的 `.run()` 函数。

### [](https://www.breezedeus.com/article/ai-agent-part2#5f29a6c7773344e69db34e3d21e0dad4 "记忆（Memory）")记忆（Memory）

**Message**：

记忆中记录的原始单元，主要记录动作执行后产生的结果。相当于斯坦福Generative Agents中的**Observation**：

每个角色执行动作后，就会产生新的记忆Message。

### [](https://www.breezedeus.com/article/ai-agent-part2#c3628338928141b1932631f9bed54292 "Environment")**Environment**

### [](https://www.breezedeus.com/article/ai-agent-part2#12a7e0f32cb744ebbcf7d9b71c49377c "角色（Roles）")角色（Roles）

**角色** **`Role`** 定义：

每个角色的 **`.run()`** 中的流程：

![notion image](https3A2F2Fs3-us-west-2.amazonaws.com2Fsecure.notion-static.com2Fe0fe797a-c912-48e7-ade2-91ac8c173dc72FUntitled.png)

当某个角色有**多个可选动作**时（`**len(self._actions)>1**`），使用以下的prompt让LLM来选择该执行哪个动作，其中 `**{history}**` 包含前面所有动作的输出结果，`**{states}**` 就是可选的动作列表：

#### [](https://www.breezedeus.com/article/ai-agent-part2#5dd141b6958a479c90e4449fc563ce78 "ProductManager")ProductManager

**Action** `**WritePRD**` 使用的 prompt 模板：**Action** `**WritePRD**` 的一个真实 prompt**：**对应的真实输出：

#### [](https://www.breezedeus.com/article/ai-agent-part2#738edc3341e848dd8de7f52abd59341e "Architect")Architect

**Action** **`WriteDesign`** 使用的 prompt 模板：**Action** **`WriteDesign`** 的一个真实 prompt**：**对应的真实输出：

#### [](https://www.breezedeus.com/article/ai-agent-part2#835295d56ba74050b4e0094c71b9bc3d "ProjectManager")ProjectManager

**Action** `**WriteTasks**` 使用的 prompt 模板：**Action** `**WriteTasks**` 的一个真实 prompt**：**对应的真实输出：

#### [](https://www.breezedeus.com/article/ai-agent-part2#862828aa6f504463a4d3865bcd635e6f "Engineer")Engineer

**Action** `**WriteCode**` 使用的 prompt 模板：和之前的一般实现不同，**`Engineer`** 有很多单独的代码，做了很多独特的事。**`Engineer`** 每次调用 `**WriteCode**` **只生成一个文件的代码**，按文件列表的顺序逐个生成所有文件的代码。之前的 `context` 只使用了角色 watch 的动作的结果，而**`Engineer`**传入 `**WriteCode**` 的 `context` 包含前面所有动作的输出结果，以及当前已生成的代码文件。所以这里的 **`context`** 特别长，如**：**以下是输出的 **ocr.py** 文件：

## [](https://www.breezedeus.com/article/ai-agent-part2#ee3e7a68e17d4b95ac9def5dfbb9e522 "总结")总结

<table><tbody><tr><td><p>ㅤ</p></td><td><p><b>AutoGPT</b></p></td><td><p>GPT-Engineer</p></td><td><p><b>Generative Agents</b></p></td><td><p><b>MetaGPT</b></p></td></tr><tr><td><p><b>场景</b></p></td><td><p>个人小助理</p></td><td><p>职业/项目场景</p></td><td><p>生活场景</p></td><td><p>职业/项目场景</p></td></tr><tr><td><p><b>Agents数量</b></p></td><td><p>单</p></td><td><p>单</p></td><td><p>多</p></td><td><p>多</p></td></tr><tr><td><p><b>环境（Environment）</b></p></td><td><p>-</p></td><td><p>-</p></td><td><p>其他Agents + 外部世界</p></td><td><p>其他Agents</p></td></tr><tr><td><p><b>与用户交互量</b></p></td><td><p>无</p></td><td><p>少</p></td><td><p>少</p></td><td><p>无</p></td></tr><tr><td><p><b>记忆（Memory）</b></p></td><td><p>短期</p></td><td><p>短期</p></td><td><p>短期 + 长期</p></td><td><p>短期为主</p></td></tr><tr><td><p><b>Agents的动作执行顺序</b></p></td><td><p>-</p></td><td><p>-</p></td><td><p>并行</p></td><td><p>串行</p></td></tr><tr><td><p><b>动作空间</b></p></td><td><p>小</p></td><td><p>-</p></td><td><p>大</p></td><td><p>小</p></td></tr><tr><td><p><b>输入和输出格式</b></p></td><td><p>偏结构化</p></td><td><p>偏结构化</p></td><td><p>偏自然语言</p></td><td><p>偏结构化</p></td></tr><tr><td><p><b>动作轮次</b></p></td><td><p>少</p></td><td><p>-</p></td><td><p>多</p></td><td><p>少</p></td></tr><tr><td><p><b>对反思与规划的要求</b></p></td><td><p>高</p></td><td><p>低</p></td><td><p>高</p></td><td><p>低；goal 和 plan 基本都事先定好</p></td></tr><tr><td><p><b>Agents之间如何交互</b></p></td><td><p>-</p></td><td><p>-</p></td><td><p>对话</p></td><td><p>获取其他agent执行动作所产生的结果</p></td></tr></tbody></table>

## [](https://www.breezedeus.com/article/ai-agent-part2#72126484132b4fcf8799d82658095750 "分享视频")**分享视频**

[**Youtube**](https://youtu.be/JuXi1hSEJfI)

![Video preview](hqdefault.jpg)

[**Bilibili**](https://www.bilibili.com/video/BV1dh4y127zz/)

## [](https://www.breezedeus.com/article/ai-agent-part2#bc120683610f4f69b55dc465fb738a86 "References")References

1.  [大模型下半场，关于Agent的几个疑问](https://mp.weixin.qq.com/s/tXxCEtAA_W1eS0ti-Yydxg)

2.  [LLM Powered Autonomous Agents | Lil'Log](https://lilianweng.github.io/posts/2023-06-23-agent/)

3.  [Generative Agents: Interactive Simulacra of Human Behavior](https://github.com/joonspk-research/generative_agents)

4.  [](https://github.com/Significant-Gravitas/Auto-GPT)

5.  [](https://github.com/AntonOsika/gpt-engineer)

6.  [](https://github.com/geekan/MetaGPT)

[GPT-4 新的超能力](https://www.breezedeus.com/article/gpt4)[解决超难问题的 Least-to-Most Prompt 框架](https://www.breezedeus.com/article/llm-prompt-l2m)
