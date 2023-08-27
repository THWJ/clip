---
title: '深入了解数据库：PostgreSQL'
date: 2023-08-24T03:06:28.000Z
updated: 2023-08-24T03:06:28.000Z
taxonomies:
  tags:
    - Tech
extra:
  source: https://www.ibm.com/blog/database-deep-dives-postgresql/
  hostname: www.ibm.com
  author: Josh Mintz
  original_title: 'Database Deep Dives: PostgreSQL - IBM Blog'
  original_lang: en

---

## In the latest installment of Database Deep Dives, we caught up with Brad Nicholson and Dave Cramer to hear about their journeys in the PostgreSQL world.  

在最新一期的Database Deep Dives中，我们采访了布拉德Nicholson和Dave Cramer，了解了他们在PostgreSQL世界的旅程。

Dave ([@dave\_cramer](https://twitter.com/dave_cramer)), from [Crunchy Data](https://www.crunchydata.com/), is the maintainer of the PostgreSQL JDBC driver. Brad, from IBM, is an Architect and Engineer for the [IBM Cloud Databases portfolio](https://www.ibm.com/cloud/databases).  

来自Crunchy Data的Dave（@dave\_cramer）是PostgreSQL JDBC驱动程序的维护者。布拉德来自IBM，是IBM Cloud Databases产品组合的架构师和工程师。

![Database Deep Dives: PostgreSQL](DatabaseDeepDives_PostgreSQL-01.png)

Read the interview below to learn how the [PostgreSQL](https://www.ibm.com/cloud/learn/postgresql) community can be its greatest strength—but also, sometimes, a weakness—and how the new pluggable storage engine can help take Postgres from a database to an application development platform.  

阅读下面的采访，了解PostgreSQL社区如何成为其最大的优势-但有时也是一个弱点-以及新的可插拔存储引擎如何帮助Postgres从数据库到应用程序开发平台。

### Tell us a little about yourself and what you are working on today?  

告诉我们一些关于你自己的事情以及你今天在做什么？

**Dave Cramer (DC):** I currently live in a small town in Ontario, Canada, and I have been fortunate enough to work at home all of my career. For fun and excitement, I like to explore my current understanding of physics on a race track with my car.  

Dave Cramer（DC）：我目前住在加拿大安大略省的一个小镇上，我很幸运地在我的职业生涯中一直在家工作。为了好玩和刺激，我喜欢在赛道上用我的车探索我目前对物理学的理解。

As to what I’m working on today, Crunchy Data has allowed me to work on Postgres full time and that’s really, really cool. I’m currently working on the [JDBC driver](https://jdbc.postgresql.org/), fixing bugs; and actually, as we speak, adding something to the backend of PostgreSQL to help the JDBC driver—and other drivers—deal with things like people changing the search path on them.  

至于我今天的工作，Crunchy Data让我可以全职工作在Postgres上，这真的很酷。我目前正在开发JDBC驱动程序，修复bug;实际上，正如我们所说的，在PostgreSQL的后端添加一些东西来帮助JDBC驱动程序和其他驱动程序处理诸如人们更改搜索路径之类的事情。

I also help out with the [PL/R procedural language](https://www.postgresql.org/docs/current/external-pl.html) that Joe Conway wrote (who also works for Crunchy Data). There are a bunch of other interesting technologies that I’m helping out with or getting involved with. One of my favorites is Logical decoding, which enables Change Data Capture in a unique way that only Postgres can do. More recently in the Java PostgreSQL world, there are a number of reactive/async drivers that I’m very interested in.  

我还帮助Joe Conway编写的PL/R过程语言（他也为Crunchy Data工作）。还有很多其他有趣的技术，我正在帮助或参与其中。我最喜欢的一个是逻辑解码，它以一种只有Postgres才能做到的独特方式实现更改数据捕获。最近在Java PostgreSQL世界中，有许多我非常感兴趣的反应/异步驱动程序。

**Brad Nicholson (BN):** I live in Toronto. Today, I’m working on IBM Cloud Databases. I’m an Architect and an Engineer on that, working in the Postgres space and across other databases as well. Really dealing with the challenges of bringing a database-as-a-service from its internal homegrown solution to a full-blown, [Kubernetes](https://www.ibm.com/cloud/learn/kubernetes)\-native platform and product.   

布拉德Nicholson（BN）：我住在多伦多。今天，我正在研究IBM Cloud Databases。我是一名架构师和工程师，在Postgres空间和其他数据库工作。真正应对将数据库即服务从其内部自主开发的解决方案转变为成熟的Kubernetes原生平台和产品的挑战。

### How did you get involved with PostgreSQL?  

你是如何参与PostgreSQL的？

**BN:** Completely by accident. I started my career as a web developer. The stuff I was working on was MySQL (back in the days before transactions existed), and there was all sorts of weird stuff happening, like columns were getting truncated silently, people would stop their browser in that day and get one table written to and not the other one. I was thinking, there has got to be a better way than this, and that was right around the time that Postgres was becoming a viable open source product.  

BN：完全是意外。我开始了我的职业生涯作为一个Web开发人员。我正在研究的东西是MySQL（回到事务存在之前的日子），并且有各种奇怪的事情发生，比如列被悄悄地截断，人们会停止他们的浏览器，并得到一个表而不是另一个表。我在想，一定有一个比这更好的方法，那是在Postgres成为一个可行的开源产品的时候。

I can’t remember exactly what version that would have been, but folks like Tom Lane had taken it over and started doing a lot of work on it. So, I switched on over to that and it fixed my problems pretty quickly because it works like you expected it to. From there, I got moved to a Postgres DBA job and went from there.   

我不记得确切的版本是什么，但像汤姆·莱恩这样的人已经接管了它，并开始在它上做了很多工作。所以，我切换到它，它很快就解决了我的问题，因为它的工作方式就像你期望的那样。从那里，我被转移到Postgres DBA工作，并从那里开始。

**DC:** It was pretty much by accident, kind of . . . maybe. There is a bit of a story here—back around 1998, I quit my job to be a consultant. The contract was supporting a Java application, and, at that time, that meant getting a Microsoft Network subscription.  

DC：这几乎是偶然的，有点。. .也许吧。这里有一个小故事--大约在1998年，我辞去了我的工作，成为了一名顾问。该合同支持Java应用程序，在当时，这意味着获得Microsoft Network订阅。

I had an issue and called up support and they said it would be three weeks. I went, “Huh, how is that going to work?” I was getting paid by the hour so three weeks seemed a little long time. I thought there has to be a better way, and I started looking at open source.  

我有一个问题，打电话给支持，他们说这将是三个星期。我想，“哈，这怎么能行得通呢？“我是按小时计酬的，所以三个星期似乎有点长。我认为一定有更好的方法，于是我开始考虑开源。

I knew nothing about it \[at first\], so I asked a friend how to get started. He said, “Go on the mailing list and start answering every question you can.” I was interested in Java, so I found the JDBC list, and I started answering every question. The first one took a couple of days to figure out, the second one took a little bit less, and by a month or two later, I could answer questions without doing the research.  

“我不知道，”他说，“我问一个朋友，他是怎么开始的。他说：“去邮件列表，开始回答你能回答的每一个问题。我对Java很感兴趣，所以我找到了JDBC列表，并开始回答每个问题。第一个花了几天时间才弄明白，第二个花的时间少一点，一两个月后，我可以在不做研究的情况下回答问题。

At some point, the guy maintaining the JDBC driver decided to step down and Bruce Momjian asked me if I was interested in supporting it. I said, “Yep,” and I have been doing it for 20 years now. That’s how I got involved in the community.   

在某个时候，维护JDBC驱动程序的人决定辞职，布鲁斯Momjian问我是否有兴趣支持它。我说，“是的”，我已经做了20年了。这就是我如何融入社区的。

### In your opinion, what are the strengths and weaknesses of PostgreSQL?   

在您看来，PostgreSQL的优点和缺点是什么？

**DC:** Oh wow, this an interesting challenge. I think the strengths and weaknesses are in the community, not necessarily in the technology. Quoting the [Roadmap](https://www.postgresql.org/developer/roadmap/)—which I’ll summarize because it’s a bit long—it says it’s a “non-commercial, all-volunteer, free software project, and, as such, there is no formal list of feature requirements required for the development. We enjoy allowing developers to explore the topics of their choosing.” There is more, but that’s the gist of it.  

DC：哇，这是一个有趣的挑战。我认为优势和劣势都在社区，不一定在技术上。引用路线图--因为它有点长，我将对其进行总结--它说它是一个“非商业的、全自愿的、自由软件项目，因此，没有正式的开发所需的特性需求列表。我们喜欢让开发人员探索他们选择的主题。”还有更多，但这就是它的要点。

I see the advantage in some ways because the project tends to not get locked into a specific solution because there is a company marketing that specific solution. Because it’s completely open source, when we realize what we have been doing is wrong or there is a better way to do it, we have no vested interested in maintaining the status quo. So, we give it up and change our path.  

我在某些方面看到了优势，因为项目往往不会被锁定在特定的解决方案中，因为有一家公司在营销特定的解决方案。因为它是完全开源的，当我们意识到我们一直在做的是错误的，或者有更好的方法来做，我们没有既得利益维持现状。所以，我们给予它，改变我们的道路。

To give you a concrete example, a few years ago, there was a de-facto standard for replication, which was a trigger-based solution. It had a lot of challenges, and since then, the community developed something called logical replication which has superseded trigger-based replication. We now have a much better solution.  

给予一个具体的例子，几年前，有一个事实上的复制标准，它是一个基于触发器的解决方案。它有很多挑战，从那时起，社区开发了一种称为逻辑复制的东西，它已经取代了基于触发器的复制。我们现在有了一个更好的解决方案。

In my opinion, the strength is also actually a weakness—the notion that we have this big project and all these different solutions. Typically, in a company-developed product, there is one way to do a specific thing and that’s the only way.  

在我看来，优势实际上也是一个弱点--我们有这个大项目和所有这些不同的解决方案的概念。通常情况下，在公司开发的产品中，有一种方法可以做一件特定的事情，这是唯一的方法。

In PostgreSQL, there are 10 or 15 ways to do something. And right now, Postgres is enjoying considerable uptake in adoption, and that means there are a lot of new people to the project trying to navigate what is the right way to do something. There may not be a right way, but there may be a whole bunch of wrong ways.  

在PostgreSQL中，有10或15种方法可以做一些事情。现在，Postgres正在享受相当大的采用，这意味着有很多新的人试图导航什么是做某事的正确方法。可能没有正确的方法，但可能有一大堆错误的方法。

For someone used to commercial software, where there is one supported solution, figuring out how to architect your solution using Postgres can be pretty challenging. The good thing about this, for me and Crunchy Data, is that this presents an opportunity for companies like Crunchy Data to provide support for known working solutions (at least known working solutions that we understand and can support.) \[That’s why\] I see it as both a strength and a weakness.  

对于那些习惯于商业软件的人来说，在只有一个支持的解决方案的情况下，弄清楚如何使用Postgres构建解决方案可能是一件非常具有挑战性的事情。对我和Crunchy Data来说，这件事的好处是，这为Crunchy Data这样的公司提供了一个机会，为已知的工作解决方案提供支持（至少是我们理解并可以支持的已知工作解决方案）。\[That这就是为什么\]我认为这既是一种优势，也是一种弱点。

**BN:** Community is one of the strengths, for sure. Dovetailing off that a bit is the licensing. There has been a lot of stuff in the news recently about open source licensing with Mongo, Redis, and Elasticsearch.  

BN：社区是优势之一，这是肯定的。除了这一点，还有许可证。最近有很多关于Mongo、Redis和Elasticsearch的开源许可的新闻。

In Postgres, the license is open—people can’t change it or take things away from it. Nobody can buy Postgres; it’s going to be an open source project as it is as long as it exists. That’s a huge, huge benefit.  

在Postgres中，许可证是开放的--人们不能更改它或拿走它的东西。没有人能买Postgres;它将是一个开源项目，因为它存在。这是一个巨大的，巨大的好处。

On the more technical side, as well as an obvious and boring thing, is stability. It’s by and large a rock-solid database as long as you stay away from some of the bleeding-edge things that might have a few edge cases in them.  

在更技术的方面，以及一个明显和无聊的事情，是稳定性。只要您远离一些可能包含一些边缘案例的前沿事物，它基本上是一个坚如磐石的数据库。

\[It’s also\] very secure. One of things I really like about it—especially compared to most databases—is that predictability of it. By and large, it’s quite predictable in how it works and how it fails. The predictability in how it fails is a really, really nice, especially when you are getting into automating solutions on for it. The lack of predictability is one of the biggest challenges I see in some of the other databases I work with (too many strange edge cases).  

\[It也很安全。我非常喜欢它的一点--特别是与大多数数据库相比--是它的可预测性。总的来说，它的工作方式和失败方式都是可以预测的。它如何失败的可预测性是非常非常好的，特别是当你开始自动化解决方案时。缺乏可预测性是我在使用的其他一些数据库中看到的最大挑战之一（太多奇怪的边缘情况）。

The other thing is extensibility. When you look at the extension system, the type of stuff that you can build on top of Postgres without forking the main codebase is actually kind of remarkable. You take a look at this thing that started its life as a relational database over 30 years ago and is now moving towards being an application development platform or really even a database development platform. That’s really cool.   

另一个是可扩展性。当你看到扩展系统时，你可以在Postgres上构建的东西，而不需要分叉主代码库，这类东西实际上是很了不起的。您可以看看这个东西，它在30多年前作为关系数据库开始了它的生命，现在正朝着应用程序开发平台甚至是数据库开发平台的方向发展。真的很酷

On weaknesses, one of the things we’re starting to see more and more is the lack of a native scale-out story like native sharding that allows larger workloads to run on Postgres natively.  

在弱点方面，我们越来越多地看到的一件事是缺乏一个原生的横向扩展故事，如原生分片，允许更大的工作负载在Postgres上原生运行。

I think the connection model is also really limiting. This whole per-process connection thing and using external connection poolers; we have third-party tools that work for that but they don’t tend to work well with multi-tenancy because you have to relax your security model at some point due to needing to keep the total number of connections relatively low and not being able to pool connections between database users.  

我认为连接模式也确实有局限性。这整个流程连接的事情和使用外部连接池;我们有第三方工具可以解决这个问题，但它们往往不能很好地与多租户一起工作，因为你必须在某个时候放松你的安全模型，因为你需要保持相对较低的连接总数，并且不能在数据库用户之间共享连接。

The logical decoding and native Postgres logical replication is really cool, as well. I think there is a big hole there right now—it doesn’t actually work all that well with streaming replication. You can’t switchover or failover a member and have it sync your place. It’s really nice for building downstream systems to consume changes off them but as soon as you have to switchover or failover, you lose your place. You have to think about re-syncing your systems, and that gets messy.  

逻辑解码和本地Postgres逻辑复制也很酷。我认为现在有一个很大的漏洞-它实际上并没有很好地与流复制一起工作。您无法切换或故障转移成员并使其同步您的位置。构建下游系统来使用它们的更改确实很好，但是一旦您必须切换或故障转移，您就失去了位置。你必须考虑重新同步你的系统，这会变得混乱。

The final one I’ll mention is an overreliance on external tooling to do a lot of basic stuff properly. Postgres gives you this rock-solid database with hooks to deploy backups, replicate, etc., but it’s up to you to put the solution together. I think Dave touched on this earlier, it can be convoluted to do that. You have to have a lot of knowledge to put together a reliable Postgres deployment, use a DbaaS solution, or pay people to do it for you.  

最后我要提到的是过度依赖外部工具来正确地完成许多基本工作。Postgres为您提供了这个坚如磐石的数据库，并带有钩子来部署备份、复制等但解决方案还是要靠你自己我想戴夫早些时候提到了这一点，这样做可能会很复杂。你必须有大量的知识来整合一个可靠的Postgres部署，使用一个DbaaS解决方案，或者付钱让人为你做。

I think especially if you look at more modern databases, it’s really not that tough to set up replication and have failover and all that stuff. It’s a bit of configuration, it’s built in the system and kind of just works.   

我认为，特别是如果您查看更现代的数据库，设置复制和故障转移等功能并不那么坚韧。这是一个小配置，它是内置在系统中的，只是工作。

### Speaking of modern databases, PG 12 is coming out pretty soon. What are you looking forward to there?  

说到现代数据库，PG 12很快就要出来了。你在那里期待什么？

**DC:** It dovetails into what I said earlier about the cool, new features and all the different itches people scratch. One of the things that come about is basically the basis for the next, sort-of jump in Postgres’s ability—the pluggable table storage interface. It’s the “developer cool thing” I’m interested in.  

DC：它与我之前所说的很酷的，新的功能和人们挠的所有不同的痒相吻合。其中一件事基本上是Postgres能力的下一个跳跃的基础--可插入的表存储接口。这是我感兴趣的“开发者酷的东西”。

Since the beginning, sort of the way Postgres does things—in one version, we’ll start the framework of a feature and it won’t be particularly useful but the next version will be a little more useful, \[and the one after that will be even more useful.\] Pluggable table storage interface is going to enable columnar storage, encrypted columns, and other domain-specific storage systems. In addition, we are starting to see improvements in partitioning. We are adding functionality to partitioning in each major version. This will enable PostgreSQL to handle much larger workloads.  

从一开始，有点像Postgres做事的方式--在一个版本中，我们将启动一个特性的框架，它不会特别有用，但下一个版本会更有用，\[之后的版本会更有用\]。Pluggable table storage接口将支持列式存储、加密列和其他特定于域的存储系统。此外，我们开始看到分区方面的改进。我们正在每个主要版本中添加分区功能。这将使PostgreSQL能够处理更大的工作负载。

**BN:** Pluggable table storage for me as well. That’s kind of the really exciting thing for Postgres. I mentioned the extensibility bit earlier and this dovetails into that, right? Once you start looking at combining extensions and pluggable table storage together, you have this development platform where you can start building all sorts of cool stuff on top of there.  

BN：对我来说也是可插拔的表存储。这对Postgres来说是一件非常令人兴奋的事情。我之前提到了可扩展性，这与此相吻合，对吗？一旦你开始考虑将扩展和可插拔表存储结合在一起，你就有了这个开发平台，你可以在这个平台上开始构建各种很酷的东西。

Another thing, which is more developer-centric, is the JSON path. Postgres has really awesome JSON capabilities. But if you aren’t a Postgres user and you come to it from using a document store, it’s going to be really weird to use. The JSON path gets closer to being able to work with JSON in Postgres in a way that developers should find more friendly.   

另一个更以开发人员为中心的是JSON路径。Postgres有很棒的JSON功能。但是如果你不是Postgres用户，而是从使用文档存储来使用它，那么使用起来会很奇怪。JSON路径更接近于能够在Postgres中使用JSON，开发人员应该会发现更友好的方式。

### What advice would you give people to want to deploy PostgreSQL on Kubernetes?  

对于想要在Kubernetes上部署PostgreSQL的人们，你会给予什么建议？

**BN:** Don’t. Seriously, everyone wants to right now because it’s the buzz technology. It definitely solves a certain set of problems, but it introduces another set of them. It’s all about tradeoffs and understanding the ones you need to make.    

BN：不要。说真的，每个人都想现在，因为它的嗡嗡声技术。它确实解决了一系列问题，但它引入了另一系列问题。这都是关于权衡和理解你需要做的。

You have to really ask yourself why you want to run it. You need to really understand what you are buying when you move into the Kubernetes world. Coming from a more standard deployment profile, you are totally changing your deployment platform— how things get deployed, how things move around.  

你得好好问问自己，为什么要经营它。当你进入Kubernetes世界时，你需要真正了解你在购买什么。从一个更标准的部署配置文件来看，您正在彻底改变您的部署平台-如何部署，如何移动。

Chances are that you’re not running your databases in [containers](https://www.ibm.com/cloud/learn/containers) already. So, when you come to Kubernetes, you are coming to [containerization](https://www.ibm.com/cloud/learn/containerization). You are going to have to throw a lot of what you know \[around things like memory management and resource utilization\] out the window and relearn it all. It’s a really big undertaking.  

很可能您还没有在容器中运行数据库。所以，当你来到Kubernetes时，你就来到了容器化。你将不得不把你所知道的很多东西（比如内存管理和资源利用）抛到九霄云外，重新学习。这是一个非常大的事业。

You also likely need to be comfortable cracking open Kubernetes source code and figuring out why it’s doing what you don’t think it should be doing (because it will sometimes).  

您可能还需要轻松地破解开放的Kubernetes源代码，并弄清楚为什么它在做您认为它不应该做的事情（因为它有时会这样做）。

From there, if you want to forge ahead with it, don’t reinvent the wheel. Basically, there are a couple operators out there (there is a plug for Dave there, [Crunchy has a Postgres Operator](https://operatorhub.io/operator/postgresql)) and Zalando, who do Patroni (which we love), also have a [Postgres Operator](https://operatorhub.io/operator/postgres-operator). So, if you really want to do it, take a look at those operators and work from there. Don’t start from scratch.  

从那里开始，如果你想继续前进，不要重新发明轮子。基本上，有几个运营商在那里（有一个插头戴夫在那里，Crunchy有一个Postgres运营商）和Zalando，谁做Patroni（我们喜欢），也有一个Postgres运营商。所以，如果你真的想这样做，看看这些操作符，然后从那里开始工作。不要从头开始。

**DC:** As opposed to don’t, I would say call Crunchy Data. You know, Kubernetes was initially designed for stateless workloads. It certainly presents a challenge when you are working with PostgreSQL; the two have some impedance mismatches.  

DC：与不要相反，我会说调用Crunchy Data。Kubernetes最初是为无状态工作负载设计的。当您使用PostgreSQL时，这无疑是一个挑战;两者具有一些阻抗失配。

Crunchy Data has deep insight into the Kubernetes world and deep insight into Postgres world. As Brad pointed out, trying to do this on your own is pretty daunting. You have to be a master of two worlds here! One person doing both is quite a challenge. If you are trying to run it on Kubernetes, you have to either hire someone or call us.   

Crunchy Data对Kubernetes世界有着深刻的洞察，对Postgres世界有着深刻的洞察。正如布拉德所指出的，试图自己做到这一点是相当艰巨的。你必须是两个世界的主人！一个人同时做这两件事是一个相当大的挑战。如果你试图在Kubernetes上运行它，你必须雇用某人或打电话给我们。

**BN:** Adding one more thing—the blogosphere has tons of stuff about running databases on Kubernetes. They are very narrowly focused on Day 1: Standing up a database. That stuff is easy these days. It’s everything that happens after that—the lifecycle of the database—that gets very difficult.  

BN：还有一件事-博客圈有大量关于在Kubernetes上运行数据库的东西。他们非常专注于第一天：建立数据库。现在这东西很容易在那之后发生的一切--数据库的生命周期--变得非常困难。

**DC:** Same thing, we have solutions to many problems. If you want to get just get a database running, that’s fine. But if you want to keep it running, that’s a much bigger problem. Kubernetes might just decide to shut down your pods for instance. Reschedule a running Postgres—we have solutions for those sorts of things. I’ll tell you, there was hair pulled to find those things. I’ll reiterate what Brad said: “Don’t reinvent the wheel.”   

DC：同样的事情，我们有很多问题的解决方案。如果你只想让数据库运行，那很好。但如果你想让它继续运行，那是一个更大的问题。例如，Kubernetes可能会决定关闭你的pod。重新安排一个运行的Postgress-我们有解决方案来解决这类问题。我告诉你，为了找到那些东西，有人拔了头发。我重申布拉德说的话：“不要重新发明轮子。

### Running on Kubernetes by yourself might be one mistake, what are the other top mistakes people make with PostgreSQL?  

自己在Kubernetes上运行可能是一个错误，那么人们在使用PostgreSQL时会犯的其他主要错误是什么？

**BN:** I would say the top one is not using a connection pooler and not understanding the Postgres connection model and its limitations. People fire up 20 copies of their application. Each one tries to open couple hundred connections each, and the next thing you know, you are running out of connections or hitting performance problems. You have to understand how the connection model in Postgres works and use a pooler like [PgBouncer](https://pgbouncer.github.io/) to bring things down to a more manageable number.  

BN：我认为最重要的一点是没有使用连接池程序，不理解Postgres连接模型及其局限性。人们打开了20份申请表。每一个都尝试打开几百个连接，接下来你知道的是，连接耗尽或遇到性能问题。您必须了解Postgres中的连接模型是如何工作的，并使用像PgBouncer这样的池器来将事情降低到一个更易于管理的数字。

**DC:** Sort of the same thing. I think it depends on the scale of the project. There are some large projects that would have benefited from some preliminary architectural consulting. They aren’t database experts (and specifically not Postgres experts).  

DC：差不多。我认为这取决于项目的规模。有一些大型项目可以从一些初步的建筑咨询中受益。他们不是数据库专家（尤其不是Postgres专家）。

I actually had someone call me the other day about an IoT project, and the guy had a particular solution in mind that I knew just wouldn’t work. He had a naive, simple solution that was going to fail. Reading, researching, or calling someone up that has that kind of knowledge (and saying, “This is what I want to do, what tools are available to do it?”) will go a long way at the beginning of a project.  

事实上，前几天有人打电话给我谈一个物联网项目，那个人脑子里有一个特别的解决方案，我知道这是行不通的。他有一个天真、简单的解决方案，但却要失败。阅读、研究或打电话给有这方面知识的人（并说：“这是我想做的，有什么工具可以做？“）在一个项目的开始会起到很大的作用。

Certainly, on a smaller scale, if you aren’t trying to make something architecturally challenging, learning how to tune Postgres. At a minimum, reading the documentation on settings and security would go a long way to making your life easier. We have an amazing documentation site, and it just appears not a lot of people read it. I guess it’s kind of like trying to eat an elephant, where do you start? But I think some reading goes a long way.   

当然，在更小的范围内，如果您不想在架构上做出具有挑战性的东西，那么学习如何调优Postgres。至少，阅读有关设置和安全性的文档将大大有助于使您的生活更轻松。我们有一个令人惊叹的文档站点，只是看起来没有多少人读它。我想这有点像试图吃大象，你从哪里开始？但我认为一些阅读会有很长的路要走。

### Do you have any secret performance tuning tips or tricks?  

你有什么秘密的性能调优技巧或技巧吗？

**BN:** I don’t think there are any secret performance tuning tips. The ones that I would say to people are:   

BN：我不认为有任何秘密的性能调优技巧。我想对人们说的是：

1.  Learn how to read a query plan and tune your queries.  
    
    了解如何读取查询计划和优化查询。
2.  Adjust your data models.  
    
    调整数据模型。
3.  Fix bad access patterns.  
    
    修复错误的访问模式。

Honestly, in my experience, you can tune knobs to make things change in the planner, add more memory, those types of things. But, by and large, the biggest wins come from fixing bad queries and fixing bad access patterns properly. To that end, install the [pg\_stat\_statements](https://www.postgresql.org/docs/11/pgstatstatements.html) extension and learn how to use it. Analyze your access pattern, validate your access patterns. Do it in an iterative fashion—don’t just do it once and forget about it. Do it as your product evolves.  

老实说，根据我的经验，你可以调整旋钮，使事情在计划器中改变，增加更多的内存，这些类型的事情。但是，总的来说，最大的胜利来自于正确地修复错误的查询和修复错误的访问模式。为此，安装pg\_stat\_statements扩展并学习如何使用它。分析你的访问模式，验证你的访问模式。以迭代的方式来做不要只做一次就忘了。随着产品的发展而做。

One of the more nuanced things—in Postgres and most databases—indexes are expensive. Postgres suffers from write amplification pretty heavily. People will throw a bunch of indexes on to handle any type of query, but they don’t realize the overall impact that has with all the writes that are driven as a part of that. So, index carefully and look for indexes you aren’t using and remove them. You can find queries on the web really easily that will find those for you.  

在Postgres和大多数数据库中，索引是比较昂贵的。Postgres受到了写入放大的严重影响。人们会抛出一堆索引来处理任何类型的查询，但他们没有意识到作为其中一部分驱动的所有写入所产生的总体影响。因此，请仔细索引，查找未使用的索引并删除它们。你可以很容易地在网络上找到查询，这将为你找到那些。

**DC:** Pretty much what Brad said. At the end of the day, in a database, the most time is taken reading and writing to disk. It’s pretty straightforward math—the I/O channel has certain bandwidth, and you’re trying to read/write a certain number of bytes on the disk, and you have a certain number of time. You can’t fix that, but you can make sure your queries are running well.  

D：和布拉德说的差不多。在一天结束时，在数据库中，最多的时间是阅读和写磁盘。这是非常简单的数学-I/O通道有一定的带宽，你试图在磁盘上读/写一定数量的字节，你有一定数量的时间。您无法修复这个问题，但可以确保您的查询运行良好。

Everybody I have seen that is good at this is vigilant and ruthless about monitoring their database. They make sure that every query they add to the code doesn’t blow up. They check for regressions when they release new code, they measure every SQL statement or instrument the app to measure it. It’s just a matter of making sure you understand what you are doing.   

我见过的每个人都擅长这一点，对监控他们的数据库都保持警惕和无情。他们确保添加到代码中的每个查询都不会爆炸。当他们发布新代码时，他们检查回归，他们测量每个SQL语句或仪器应用程序来测量它。这只是一个确保你明白你在做什么的问题。

The other big thing is their development systems and development data that they’re developing on are orders of magnitude smaller than their production data. They then get these huge surprises in production! There is a typical moment of: “Why is this not using an index?” Because the index is actually slower. It’s because they don’t have enough development data or test data to actually “test” what they are doing in production. At the end of the day, it’s common sense. Test everything, double-check it, verify it, measure it, and fix what’s broken.  

另一件大事是他们的开发系统和开发数据，他们正在开发的数据比他们的生产数据小几个数量级。然后他们在生产中得到了这些巨大的惊喜！有一个典型的时刻：“为什么不使用索引？“因为索引实际上更慢。这是因为他们没有足够的开发数据或测试数据来实际“测试”他们在生产中所做的事情。说到底，这是常识。测试所有的东西，仔细检查，验证，测量，并修复损坏的东西。

### PostgreSQL vs. MySQL: What are some things application developers should be considering as they pick a database?  

PostgreSQL与MySQL：应用程序开发人员在选择数据库时应该考虑哪些事情？   

**DC:** I’m not really familiar enough with MySQL to do justice to this question. But I can talk about what they should be aware of in Postgres. They should understand the question, “What is a transaction?” They should understand the answer to the question, “What is transaction isolation?”  

DC：我对MySQL还不够熟悉，无法回答这个问题。但我可以谈谈他们在Postgres中应该注意的事情。他们应该理解这个问题，“什么是交易？“他们应该理解“什么是事务隔离？“

What we’re seeing today in big applications is that the application framework itself is pretty big. They are large, complex frameworks that take time and effort to master in their own right. They tend to look at the database as sort of a “dumb” store. They don’t really pay attention to it until it does something they didn’t expect. So, I think they should at least be aware of what a transaction is and understand what transaction isolation is. They should call someone . . . Crunchy Data would be glad to help.   

我们今天在大型应用程序中看到的是，应用程序框架本身相当大。它们是大型而复杂的框架，需要时间和精力来掌握它们本身的权利。他们倾向于将数据库视为一种“愚蠢”的存储。他们不会真正关注它，直到它做了一些他们没有预料到的事情。所以，我认为他们至少应该知道什么是事务，并理解什么是事务隔离。他们应该打电话给别人。. . Crunchy Data很乐意提供帮助。

**BN:** I don’t have too much to contribute here because I don’t know too much about MySQL from an app-development perspective. I haven’t used it in that context in a very long time and it has changed a lot.   

BN：我在这里没有太多的贡献，因为从应用程序开发的角度来看，我对MySQL了解不多。我已经很长一段时间没有在这种情况下使用它了，它已经改变了很多。

### Wrapping it up, where do you see Postgres going in the next 5-10 years?  

总而言之，你认为Postgres在未来5-10年内会走向何方？

**DC:** That’s a really good question, which means I really don’t have an answer. I do think there are some things we can look at.  

DC：这是一个非常好的问题，这意味着我真的没有答案。我认为有些事情我们可以看看。

I can give you some guesses; we have overcome the stigma of using open source in big businesses. I would be willing to bet that there isn’t a Fortune 500 company out there without a Postgres running it in somewhere. What this means is that its popularity is going to increase geometrically. The more people that use it, the more people that tell their friends. And the more they tell their friends, the more people use it. What that means to the project is that we are going to have more people working on the codebase.  

我可以给予你一些猜测;我们已经克服了在大企业中使用开源的耻辱。我敢打赌，没有一家财富500强公司没有Postgres在某个地方运行。这意味着它的受欢迎程度将呈几何级数增长。越多的人使用它，越多的人告诉他们的朋友。他们告诉朋友的越多，人们就越多。这对项目意味着我们将有更多的人在代码库上工作。

One of things I find working in the open source community is how smart other people are. It’s kind of humbling. There are some brilliant people out there that are going to solve some of the hard problems we have today. The biggest challenge is that the community is going to have to figure out how to deal with more people. I don’t know what the future brings, but I know we will have more people.  

我发现在开源社区工作的一件事是其他人有多聪明。这有点让人羞愧。有一些杰出的人将解决我们今天面临的一些困难问题。最大的挑战是社区将不得不弄清楚如何与更多的人打交道。我不知道未来会发生什么，但我知道我们会有更多的人。

**BN:** I want to add to what Dave there, that’s a really good point. I think there is going to be friction with how Postgres does stuff—they have their own way of doing things that’s different from the modern GitHub-style workflow most folks are accustomed to these days. There is nothing wrong with that, but it’s a higher barrier of entry for folks coming from GitHub workflows and that type of stuff.  

BN：我想补充一下戴夫，这是一个非常好的观点。我认为Postgres的工作方式会有摩擦--他们有自己的做事方式，与大多数人现在习惯的现代GitHub风格的工作流程不同。这并没有什么错，但对于来自GitHub工作流和这类东西的人来说，这是一个更高的进入门槛。

There will be some challenges there. I think as a database in general, no one can predict the future. But if you look at where it’s come from, it’s come from being an academic relational database to a solid, open source relational database to a mixed-model system with relational and non-relational stuff.  

那里会有一些挑战。我认为作为一个数据库，没有人可以预测未来。但如果你看看它的来源，它从一个学术关系数据库到一个坚实的，开源的关系数据库，再到一个包含关系和非关系的混合模型系统。

When you start looking at the pluggable table storage and the extension framework, I think you will start to see Postgres become even more of a swiss-army knife database. You will start seeing it handling a lot more workloads.   

当您开始研究可插拔的表存储和扩展框架时，我想您会开始看到Postgres变得更像瑞士军刀数据库。您将开始看到它处理更多的工作负载。

**Well that’s it. Thank you very much to Brad and David for joining us and sharing their thoughts on PostgreSQL. Keep an eye out for our next interview in the coming weeks.** **Special thanks to Emily Hu for help on this interview. If you haven’t already, check out our other installments:**  

就这样了非常感谢布拉德和大卫加入我们并分享他们对PostgreSQL的想法。请留意下一周我们的下一次面试。特别感谢艾米丽Hu对这次采访的帮助。如果您还没有，请查看我们的其他分期付款：

-   [Database Deep Dives: CouchDB  
    
    数据库深度挖掘：CouchDB](https://www.ibm.com/cloud/blog/database-deep-dives-couchdb)
-   [Database Deep Dives: PingCAP and TiKV  
    
    数据库深度挖掘：PingCAP和TiKV](https://www.ibm.com/cloud/blog/database-deep-dives-pingcap-and-tikv)
-   [Database Deep Dives: JanusGraph  
    
    数据库深度挖掘：JanusGraph](https://www.ibm.com/cloud/blog/database-deep-dives-janusgraph)
-   [Database Deep Dives: MongoDB  
    
    数据库深度挖掘：MongoDB](https://www.ibm.com/cloud/blog/database-deep-dives-mongodb)

## Learn more about PostgreSQL  

了解更多PostgreSQL

-   [PostgreSQL: The World’s Most Advanced Open Source Relational Database  
    
    PostgreSQL：世界上最先进的开源关系数据库](https://www.postgresql.org/)
-   [PostgreSQL Community  PostgreSQL社区](https://www.postgresql.org/community/)
-   [PostgreSQL Explained  PostgreSQL解释](https://www.ibm.com/cloud)
-   [IBM Cloud Databases for PostgreSQL](https://cloud.ibm.com/catalog/services/databases-for-postgresql)
-   [Hyper Protect DBaaS for PostgreSQL  
    
    HyperProtect DBaaS for PostgreSQL](https://cloud.ibm.com/catalog/services/hyper-protect-dbaas-for-postgresql)
