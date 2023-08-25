---
title: How ChatGPT turned generative AI into an “anything tool” ChatGPT 怎样将生成式AI变成通用工具
date: 2023-08-25T07:54:42.000Z
updated: 2023-08-25T07:54:42.000Z
taxonomies:
  tags:
    - Tech
extra:
  source: >-
    https://arstechnica.com/ai/2023/08/how-chatgpt-turned-generative-ai-into-an-anything-tool/
  hostname: arstechnica.com
  author: Haomiao Huang -  8/23/2023, 7:30 PM黄浩淼 - 2023/8/23 下午7：30
  original_title: How ChatGPT turned generative AI into an “anything tool”
  original_lang: en

---

#### do anything —  做任何事情——

## Until recently, AI models were specialized tools. Modern LLMs are different.  

直到最近，人工智能模型还是专门的工具。现代LLMs是不同的。

![How ChatGPT turned generative AI into an “anything tool”](chatgpt-anything-tool-800x450.jpg)

Aurich Lawson | Getty Images  

奥里希·劳森 |盖蒂图片社

The chief technology officer of a robotics startup told me earlier this year, “We thought we’d have to do a lot of work to build ‘ChatGPT for robotics.’ Instead, it turns out that, in a lot of cases, ChatGPT _is_ ChatGPT for robotics.”  

今年早些时候，一家机器人初创公司的首席技术官告诉我，“我们认为我们必须做很多工作来构建'机器人ChatGPT'。相反，事实证明，在很多情况下，ChatGPT是机器人的ChatGPT。

Until recently, AI models were specialized tools. Using AI in a particular area, like robotics, meant spending time and money creating AI models specifically and only for that area. For example, Google’s AlphaFold, an AI model for predicting protein folding, was trained using protein structure data and is only useful for working with protein structures.  

直到最近，人工智能模型还是专门的工具。在特定领域（如机器人技术）中使用人工智能意味着花费时间和金钱专门针对该领域创建人工智能模型。例如，谷歌的AlphaFold是一种用于预测蛋白质折叠的AI模型，它是使用蛋白质结构数据训练的，只对处理蛋白质结构有用。

So this founder thought that to benefit from generative AI, the robotics company would need to create its own specialized generative AI models for robotics. Instead, the team discovered that for many cases, they could use off-the-shelf ChatGPT for controlling their robots without the AI having ever been specifically trained for it.  

因此，这位创始人认为，要从生成式AI中受益，机器人公司需要为机器人技术创建自己的专用生成AI模型。相反，该团队发现，在许多情况下，他们可以使用现成的ChatGPT来控制他们的机器人，而无需AI专门训练过。

I’ve heard similar things from technologists working on everything from health insurance to semiconductor design. To create ChatGPT, a chatbot that lets humans use generative AI by simply having a conversation, OpenAI needed to change large language models (LLMs) like GPT3 to become more responsive to human interaction.  

我从从事从健康保险到半导体设计等各个领域的技术人员那里听到了类似的事情。为了创建ChatGPT，一个让人类通过简单地进行对话来使用生成AI的聊天机器人，OpenAI需要改变像GPT3这样的大型语言模型（LLM），以更好地响应人类互动。

But perhaps inadvertently, these same changes let the successors to GPT3, like GPT3.5 and GPT4, be used as powerful, general-purpose information-processing tools—tools that aren’t dependent on the knowledge the AI model was originally trained on or the applications the model was trained for. This requires using the AI models in a completely different way—programming instead of chatting, new data instead of training. But it's opening the way for AI to become general purpose rather than specialized, more of an “anything tool.”  

但也许无意中，这些相同的变化让 GPT3 的继任者（如 GPT3.5 和 GPT4）被用作强大的通用信息处理工具——这些工具不依赖于 AI 模型最初训练的知识或模型训练的应用程序。这需要以完全不同的方式使用AI模型 - 编程而不是聊天，新数据而不是训练。但它为人工智能开辟了道路，使其成为通用而非专用，更像是一种“任何工具”。

Now, an important caveat in a time of AI hype: When I say “general purpose” and “anything tool,” I mean in the way CPUs are general purpose vs, say, specialized signal-processing chips. They are tools that can be used for a wide variety of tasks, _not_ all-powerful and all-knowing. And just like good programmers don’t deploy code to production without code review and unit tests, AI output will need its own processes and procedures. The applications I talk about below are tools for multiplying human productivity, not autonomous agents running amok. But the important thing is to recognize what AI _can_ usefully do.  

现在，在人工智能炒作的时代，一个重要的警告是：当我说“通用”和“任何工具”时，我的意思是CPU是通用的，而不是专用的信号处理芯片。它们是可用于各种任务的工具，而不是全能和无所不知的。就像优秀的程序员不会在没有代码审查和单元测试的情况下将代码部署到生产环境中一样，人工智能输出也需要自己的流程和程序。我在下面讨论的应用程序是用于提高人类生产力的工具，而不是横行运行的自主代理。但重要的是认识到人工智能可以做什么。

So to that end, how did we get here?  

那么，我们是如何走到这一步的呢？

## Fundamentals: Probability, gradient descent, and fine-tuning  

基础知识：概率、梯度下降和微调

Let’s take a moment to touch on how the LLMs that power generative AI work and how they’re trained.  

让我们花点时间谈谈为生成式人工智能提供动力的LLM是如何工作的，以及它们是如何训练的。

LLMs like GPT4 are probabilistic; they take an input and predict the probability of words and phrases relating to that input. They then generate an output that is most likely to be appropriate given the input. It’s like a very sophisticated auto-complete: Take some text, and give me what comes next. Fundamentally, it means that generative AI doesn’t live in a context of “right and wrong” but rather “more and less likely.”  

像 GPT4 这样的 LLM 是概率性的;他们接受输入并预测与该输入相关的单词和短语的概率。然后，它们生成一个最适合给定输入的输出。这就像一个非常复杂的自动完成：拿一些文本，然后告诉我接下来会发生什么。从根本上说，这意味着生成式人工智能不是生活在“对与错”的环境中，而是“越来越不可能”。

Being probabilistic has strengths and weaknesses. The weaknesses are well-known: Generative AI can be unpredictable and inexact, prone to not just producing bad output but producing it in ways you’d never expect. But it also means the AI can be unpredictably powerful and flexible in ways that traditional, rule-based systems can’t be. We just need to shape that randomness in a useful way.  

概率有优点和缺点。弱点是众所周知的：生成式人工智能可能是不可预测和不准确的，不仅容易产生糟糕的输出，而且会以你意想不到的方式产生它。但这也意味着人工智能可以以传统的、基于规则的系统无法做到的方式变得不可预测的强大和灵活。我们只需要以一种有用的方式塑造这种随机性。

Here’s an analogy. Before quantum mechanics, physicists thought the universe worked in predictable, deterministic ways. The randomness of the quantum world came as a shock at first, but we learned to embrace quantum weirdness and then use it practically. Quantum tunneling is fundamentally stochastic, but it can be guided so that particles jump in predictable patterns. This is what led to semiconductors and the chips powering the device you’re reading this article on. Don’t just accept that God plays dice with the universe—learn how to load the dice.  

打个比方。在量子力学出现之前，物理学家认为宇宙以可预测的、确定性的方式运作。量子世界的随机性起初令人震惊，但我们学会了接受量子怪异，然后实际使用它。量子隧穿基本上是随机的，但它可以被引导，使粒子以可预测的模式跳跃。这就是导致半导体和芯片为您正在阅读本文的设备供电的原因。不要只接受上帝与宇宙玩骰子——学习如何装骰子。

The same thing applies to AI. We train the neural networks that LLMs are made of using a technique called “gradient descent.” Gradient descent looks at the outputs a model is producing, compares that with training data, and then calculates a “direction” to adjust the neural network’s parameters so that the outputs become “more” correct—that is, to look more like the training data the AI is given. In the case of our magic auto-complete, a more correct answer means output text that is more likely to follow the input.  

同样的事情也适用于人工智能。我们使用一种称为“梯度下降”的技术训练LLM的神经网络。梯度下降查看模型正在生成的输出，将其与训练数据进行比较，然后计算一个“方向”来调整神经网络的参数，使输出变得“更”正确，也就是说，看起来更像AI给出的训练数据。在我们的魔术自动完成的情况下，更正确的答案意味着输出文本更有可能跟随输入。

Probabilistic math is a great way for computers to deal with words; computing how likely some words are to follow other words is just counting, and “how many” is a lot easier for a computer to work with than “more right or more wrong.” Produce output, compare with the training data, and adjust. Rinse and repeat, making many small, incremental improvements, and eventually you'll turn a neural network that spits out gibberish into something that produces coherent sentences. And this technique can also be adapted to pictures, DNA sequences, and more.  

概率数学是计算机处理单词的好方法;计算一些单词跟随其他单词的可能性只是在计算，对于计算机来说，“多少”比“更正确或更错误”更容易使用。生成输出，与训练数据进行比较，然后进行调整。冲洗并重复，进行许多小的渐进式改进，最终你会把一个吐出胡言乱语的神经网络变成产生连贯句子的东西。这种技术也可以适用于图片、DNA序列等。

[![Illustrative example of gradient descent (or in this case, ascent) using an image AI model instead of text, showing how incremental adjustment improves the model’s performance.](genai4-980x587.png)](https://cdn.arstechnica.net/wp-content/uploads/2023/08/genai4.png)

[Enlarge](https://cdn.arstechnica.net/wp-content/uploads/2023/08/genai4.png) / Illustrative example of gradient descent (or in this case, ascent) using an image AI model instead of text, showing how incremental adjustment improves the model’s performance.  

放大/说明性示例 使用图像 AI 模型而不是文本进行梯度下降（或在本例中为上升），显示增量调整如何提高模型的性能。

Gradient descent is a big deal. It means that creating AI models is iterative. You start with a model that produces mostly wrong (less likely) output and train it until it produces mostly right (more likely) output. But gradient descent also lets you take an existing model that’s already been trained and tweak it to your liking.  

梯度下降是一件大事。这意味着创建 AI 模型是迭代的。你从一个产生大部分错误（不太可能）输出的模型开始，然后训练它，直到它产生大部分正确（更有可能）的输出。但是梯度下降也可以让你采用已经训练过的现有模型，并根据自己的喜好进行调整。

This is what enables one of the most powerful techniques in modern AI: fine-tuning. Fine-tuning is a way of using gradient descent to take an AI model that’s already been trained and specializing it in a particular way by training it on a curated set of data. The training uses gradient descent from an already working model to make the AI better at managing or producing that specific kind of data.  

这就是现代人工智能中最强大的技术之一：微调。微调是一种使用梯度下降来获取已经过训练的 AI 模型的方法，并通过在一组精选的数据集上对其进行训练，以特定方式对其进行专业化。训练使用来自已经工作的模型的梯度下降，使AI更好地管理或生成特定类型的数据。

For example, people have taken the Stable Diffusion model, which creates images from text, and fine-tuned it to be especially good at making anime images or landscapes. And of course there are people fine-tuning language models designed for text to work better with advertising copy, legal documents, and so forth.  

例如，人们采用了稳定扩散模型，该模型从文本中创建图像，并将其微调为特别擅长制作动漫图像或风景。当然，有些人会微调为文本设计的语言模型，以便更好地与广告文案、法律文件等配合使用。

[![A cartoon image showing how fine-tuning can be used to adjust an existing AI model to produce a different kind of output.](genai6-980x559.png)](https://cdn.arstechnica.net/wp-content/uploads/2023/08/genai6.png)

[Enlarge](https://cdn.arstechnica.net/wp-content/uploads/2023/08/genai6.png) / A cartoon image showing how fine-tuning can be used to adjust an existing AI model to produce a different kind of output.  

放大 / 卡通图像，显示如何使用微调来调整现有的AI模型以产生不同类型的输出。

But fine-tuning goes well beyond getting AI models to specialize in particular subject areas. It can also be used to train AI models _how_ to respond and produce output. It’s a powerful tool that has played a big role in moving generative AI forward, including the two key innovations that led to the creation of ChatGPT.  

但微调远远超出了让人工智能模型专注于特定主题领域。它还可用于训练AI模型如何响应和产生输出。这是一个强大的工具，在推动生成式人工智能向前发展方面发挥了重要作用，包括导致创建 ChatGPT 的两项关键创新。

## Innovation 1: Following commands  

创新1：以下命令

When OpenAI released GPT2 back in 2019, it was an exciting curiosity that could write realistic stories based on short prompts. For example, it wrote some cool ones about [unicorns in the Andes](https://arstechnica.com/information-technology/2019/02/researchers-scared-by-their-own-work-hold-back-deepfakes-for-text-ai).  

当 OpenAI 在 2019 年发布 GPT2 时，这是一种令人兴奋的好奇心，可以根据简短的提示编写现实的故事。例如，它写了一些关于安第斯山脉独角兽的很酷的文章。

But using GPT2 was like playing a word-association game, in that output followed input randomly but not usefully. For example, say you wanted that article about unicorns in the Andes. But what if you wanted a long-form article? Or what if you wanted a light, breezy, bulleted list instead?  

但是使用 GPT2 就像玩单词联想游戏，因为输出随机跟随输入，但没有用。例如，假设你想要那篇关于安第斯山脉独角兽的文章。但是，如果您想要一篇长篇文章怎么办？或者，如果您想要一个轻巧、轻松的项目符号列表怎么办？

Working with GPT2 was like trying to make a spray paint painting with a spray can but no stencils and with a paint nozzle that doesn't let you control the width of the spray line. It’s possible to create art, but it's very difficult to make the specific painting you have in mind.  

使用 GPT2 就像尝试使用喷雾罐但没有模板和不允许您控制喷涂线宽度的油漆喷嘴进行喷漆。创作艺术是可能的，但要制作出你心目中的特定绘画是非常困难的。

The problem of getting AI to do what a human user wants is called “AI alignment.” You might have heard people talking about the “Big-A” alignment problems of building AI into society in such a way that it aligns with our ethics and doesn’t kill us all. But there’s also a “small-A” alignment problem: How do you make the output of a generative AI system more controllable by the human user? This is also sometimes called “steerability.”  

让AI做人类用户想要的事情的问题被称为“AI对齐”。你可能听说过人们谈论将人工智能建设到社会中的“大A”对齐问题，使其符合我们的道德规范，不会杀死我们所有人。但还有一个“小A”对齐问题：如何使生成AI系统的输出更容易被人类用户控制？这有时也称为“可操纵性”。

GPT3 was a step forward from GPT2 in the length and complexity of the text that it could generate. But just as importantly, it featured a breakthrough in alignment: GPT3 could explicitly follow commands. OpenAI’s researchers realized that by fine-tuning GPT3 with examples of commands paired with responses to those commands, they could make GPT3 understand how to explicitly follow commands and answer questions.  

GPT3 在可以生成的文本的长度和复杂性方面比 GPT2 向前迈出了一步。但同样重要的是，它在对齐方面取得了突破：GPT3 可以明确地遵循命令。OpenAI的研究人员意识到，通过使用与对这些命令的响应配对的命令示例微调GPT3，他们可以使GPT3了解如何明确遵循命令并回答问题。

This is a natural extension of the “auto-complete” capability—training the AI that the next words to come after a question should be an answer rather than an extension of the question. And the next words after a command like “write me a poem” should be the poem being asked for and not a longer version of the command.  

这是“自动完成”功能的自然延伸 - 训练AI问题之后的下一个单词应该是答案而不是问题的扩展。命令后面的下一个单词，如“给我写一首诗”应该是被要求的诗，而不是命令的更长版本。

Say you want an article about scientists discovering unicorns in the Andes. Instead of simply writing a summary prompt and letting the AI fill out a few paragraphs, you could tell GPT3 explicitly, "Write a short article about scientists discovering unicorns in the Andes, in the style of a Buzzfeed list." And it would do so.  

假设你想要一篇关于科学家在安第斯山脉发现独角兽的文章。与其简单地写一个摘要提示并让AI填写几段，不如明确地告诉GPT3，“写一篇关于科学家在安第斯山脉发现独角兽的短文，以Buzzfeed列表的风格。它会这样做。

Or you could tell it, "Write an article about scientists discovering unicorns in the Andes in the style and voice of a long-form New Yorker article." And it would write something more appropriate to that prompt.  

或者你可以说，“写一篇关于科学家在安第斯山脉发现独角兽的文章，以一篇长篇《纽约客》文章的风格和声音。它会写一些更适合该提示的内容。

This was a huge step forward because it meant that controlling the AI could be done simply and directly in human language instead of writing a computer program. And OpenAI didn’t have to explicitly build in the ability to follow commands in the structure of GPT3; instead, it just built a flexible, powerful language model and fine-tuned it with examples of commands and responses.  

这是向前迈出的一大步，因为这意味着控制人工智能可以简单直接地用人类语言完成，而不是编写计算机程序。OpenAI 不必在 GPT3 的结构中明确构建遵循命令的能力;相反，它只是构建了一个灵活、强大的语言模型，并使用命令和响应的示例对其进行了微调。

## Innovation 2: Taking feedback  

创新2：接受反馈

Following commands made GPT3 a lot easier to work with than GPT2. But it was still limited. Working with an AI like this is a bit like playing a slot machine. Pull the lever (give an input), get an output. Maybe it’s good, maybe it’s not. If not, try again. But as every artist, programmer, or writer knows, that’s not how creation works. Creation, like gradient descent for AI training, is best when it’s iterative.  

以下命令使 GPT3 比 GPT2 更容易使用。但它仍然有限。与这样的AI一起工作有点像玩老虎机。拉动杠杆（给出输入），获得输出。也许是好的，也许不是。如果没有，请重试。但正如每个艺术家、程序员或作家都知道的那样，这不是创造的运作方式。创建，如 AI 训练的梯度下降，在迭代时是最好的。

The same is true of working with generative AI. If the AI produces something that’s almost right, you don’t want to start over. You want it to start from the output the AI already gave you so you can guide it from bad to good to great. You need to train the AI how to understand feedback.  

使用生成式 AI 也是如此。如果人工智能产生的东西几乎是正确的，你不想重新开始。你希望它从AI已经给你的输出开始，这样你就可以引导它从坏到好再到好。你需要训练人工智能如何理解反馈。

There is a way to do this. The input to an AI model is called the context window. You can think of the context window as the text that our magic auto-complete takes in and then continues from. One way to work with an AI is to feed its own output back into the context window so that each input isn’t just a command but a command plus a “history” to apply that command to. This way, you can get the AI to modify its past output into something better. But you need the AI to understand how to take commands to make edits and not just new output.  

有一种方法可以做到这一点。AI 模型的输入称为上下文窗口。您可以将上下文窗口视为我们的魔术自动完成功能接收然后继续的文本。使用 AI 的一种方法是将其自己的输出反馈回上下文窗口，以便每个输入不仅仅是一个命令，而是一个命令加上一个“历史记录”来应用该命令。这样，你可以让AI将其过去的输出修改为更好的输出。但是你需要人工智能了解如何获取命令进行编辑，而不仅仅是新的输出。

This is what OpenAI accomplished with a version of GPT3 called InstructGPT. To address the problem of iteration, OpenAI made GPT3 better at following commands to make changes to an existing body of text it was given. This meant training the AI to respond more like a human when receiving feedback. To do this, OpenAI applied a technique called reinforcement learning with human feedback (RLHF).  RLHF is a way of training AIs to mimic human preferences based on training examples from a human.  

这就是OpenAI通过一个名为InstructGPT的GPT3版本完成的。为了解决迭代问题，OpenAI 使 GPT3 更好地遵循命令来更改给定的现有文本正文。这意味着训练人工智能在收到反馈时更像人类一样做出反应。为此，OpenAI应用了一种称为人类反馈强化学习（RLHF）的技术。 RLHF是一种训练AI的方法，以根据人类的训练示例模仿人类的偏好。

InstructGPT introduced another new pattern to working with GPT. Instead of “here’s a command, give me an output,” it tells the AI, “Here's the previous output you gave me, here’s my feedback on what to give me next based on what you gave me before, now give me a new output.”  

InstructGPT 引入了另一种使用 GPT 的新模式。它不是“这是一个命令，给我一个输出”，而是告诉人工智能，“这是你给我的先前输出，这是我根据你之前给我的内容给我下一步给我什么的反馈，现在给我一个新的输出。

This turned working with an AI into a conversational experience; instead of command and response, it’s a conversation with history. Every time the AI produced an output, it used the history of the entire conversation so far as a basis, not just the latest command it received. It could remember what you told it before and use it as a basis for its output.  

这把与人工智能一起工作变成了一种对话体验;这不是命令和响应，而是与历史的对话。每次人工智能产生输出时，它都会使用整个对话的历史作为基础，而不仅仅是它收到的最新命令。它可以记住你之前告诉它的内容，并将其用作其输出的基础。

[![In ChatGPT, the app (ChatGPT) stores the history of the conversation. Then it takes this history, along with the new input, and feeds it to the LLM (GPT3.5 or GPT4) to generate new output. The new output takes into account both the chat history and the feedback provided by the user in the prompt.](genai2-980x563.png)](https://cdn.arstechnica.net/wp-content/uploads/2023/08/genai2.png)

[Enlarge](https://cdn.arstechnica.net/wp-content/uploads/2023/08/genai2.png) / In ChatGPT, the app (ChatGPT) stores the history of the conversation. Then it takes this history, along with the new input, and feeds it to the LLM (GPT3.5 or GPT4) to generate new output. The new output takes into account both the chat history and the feedback provided by the user in the prompt.  

放大/在ChatGPT中，应用程序（ChatGPT）存储对话的历史记录。然后，它将此历史记录与新输入一起提供给LLM（GPT3.5或GPT4）以生成新的输出。新输出会同时考虑聊天历史记录和用户在提示中提供的反馈。

Just as with obeying commands, RLHF is an example of fine-tuning. OpenAI created InstructGPT from GPT3 by fine-tuning GPT3 with example data from human testers rating the output of AIs responding to feedback. This was another big step forward in AI alignment. By making the AI good at responding to feedback, it made the workflow of using GenAI iterative.  

就像服从命令一样，RLHF是微调的一个例子。OpenAI 通过对 GPT3 进行微调，从而从 GPT3 创建了 InstructGPT，这些测试人员对响应反馈的 AI 输出进行评级。这是人工智能对齐的又一大进步。通过让AI善于响应反馈，它使使用GenAI的工作流程具有迭代性。

Analogy time again: Working with earlier AI models was like playing darts. You could adjust your form and positioning, trying to hit the bullseye, but each throw was a separate shot. You might hit the bullseye on the first throw, or you might never hit the bullseye. But with InstructGPT, it’s more like playing golf. You start each stroke from where you left off. It might take a few tries, but you’ll get in the hole eventually, or at least reach the green.

OpenAI combined InstructGPT with GPT3 to create GPT3.5. It then put GPT3.5 behind a web interface that lets anyone communicate with it from a browser, creating ChatGPT. (A pedantic but useful distinction: GPT3, GPT3.5, and GPT4 are models, neural networks that take input from a context window and produce output. ChatGPT is an application, in this case a webpage, that lets a human interact with an AI model under the hood—either GPT3.5 or GPT4—with a chat interface.)

On that day, a phenomenon was born: ChatGPT was supposed to be a research preview to test the chat interface; instead, it reached 100M users faster than any app in history. The chat interface obviously helped, but so did something else. In creating the interactive chat interface for ChatGPT, OpenAI also made GPT3.5 and its successors like GPT4 into powerful general-purpose processing tools.

## The new framework: “processing” instead of “chat”

We’ve seen how gradient descent led to fine-tuning, which led to following commands, which then led to feedback and interaction. That ultimately led to an incredibly responsive AI chatbot in the form of ChatGPT. But the breakthrough happening now is the creation of an entirely new and different framework for working with LLMs: using them not as a chatbot that a human is talking to that uses its own knowledge to produce words and answers, but rather as processing tools that can be accessed by other software to work with data the model has never seen.

Here’s how this works.

Consider the simplest, platonic ideal of a computer: a CPU, some working memory, and a program. The CPU takes the data in the working memory, follows the instructions given to it via the program, and processes that data to produce something useful (or not, depending on the skill of the programmer). The key is that the CPU is generic and general-purpose, it doesn’t have to “know” anything in particular about the data it’s working with, so the same CPU can be used with all kinds of data.

Now look at how ChatGPT works. We have an AI model (GPT4) that has the ability to take input via a context window. We also have the ability to treat part of the input as commands and part of the input as history, or memory, that the commands apply to. If we use GPT4 to power ChatGPT, we’ve created a chatbot that uses that memory for a record of the conversation it has been having.

But there’s no reason you couldn’t fill the context window—that short-term, working memory—with other information. What if, Instead of a conversation history, you gave the AI some other data to act on? Now, instead of having a conversation, you’ve turned working with the AI model into a data processing operation.

[![Using an LLM with feedback and command following now can look a lot like using a CPU to run a program.](genai3-980x382.png)](https://cdn.arstechnica.net/wp-content/uploads/2023/08/genai3.png)

[Enlarge](https://cdn.arstechnica.net/wp-content/uploads/2023/08/genai3.png) / Using an LLM with feedback and command following now can look a lot like using a CPU to run a program.

This is incredibly powerful because, unlike a CPU, the AI model can take commands in natural, human language instead of binary code. And it has enough understanding and flexibility to work with all kinds of information without the need for you to specify and explain things in detail.

Let’s translate this into some concrete, real-world examples. How would you use an LLM with working memory and a knack for following commands to do something productive?

## Example 1: Text and documents

We’ll start with the most straightforward application for a language model: handling text.

Imagine you're a health insurance company grappling with a massive amount of policy documents and customer information. You want to build an AI tool that lets users ask questions about that data and get useful answers: Does my insurance cover elective procedures? What’s my deductible? Is tattoo removal covered?

How would you go about building this?

The old approach would be to take an AI model and fine-tune that model over all of your documents and user data so it learns that information. Then a user could just ask questions of the AI directly. But this creates all sorts of difficulties, the most obvious of which is that every time there’s any sort of change, you’d have to retrain and redeploy a whole new language model! Plus, your model would know the policy information for all users. How do you keep it from telling User A about User B’s private information if User A asks?

Fortunately, there’s another way. We don’t have to rely on the model to “memorize” the information. Instead, we could give the LLM the documents and a specific user’s policy information, then command it to answer the user’s question using that specific data. But the context window is limited; we can’t feed the LLM all of the documents we have. How do we give it just the relevant information it needs to produce an answer?

The answer is to use something called "embeddings."

Remember, LLMs work with text by transforming words into math and probabilities. As a byproduct of training, these models also learn a numerical representation of how words relate to concepts and other words.

These internal numerical representations of words and concepts are called embeddings. It’s like a library filing system for words and concepts: You can look up a concept if you know its embedding, and vice versa. You can modify an LLM so that, instead of producing words, it can report to you its embedding for words and phrases. OpenAI and other AI companies often have special versions of their models to do precisely this.

Page: [1](https://arstechnica.com/ai/2023/08/how-chatgpt-turned-generative-ai-into-an-anything-tool/1/) [2](https://arstechnica.com/ai/2023/08/how-chatgpt-turned-generative-ai-into-an-anything-tool/2/) [3](https://arstechnica.com/ai/2023/08/how-chatgpt-turned-generative-ai-into-an-anything-tool/3/) 4 [5](https://arstechnica.com/ai/2023/08/how-chatgpt-turned-generative-ai-into-an-anything-tool/5/) [6](https://arstechnica.com/ai/2023/08/how-chatgpt-turned-generative-ai-into-an-anything-tool/6/) [Next →](https://arstechnica.com/ai/2023/08/how-chatgpt-turned-generative-ai-into-an-anything-tool/5/)
