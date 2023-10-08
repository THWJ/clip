---
title: GPL许可证的问题
date: 2023-10-08T07:24:57.000Z
updated: 2023-10-08T07:24:57.000Z
taxonomies:
  tags:
    - Finace
    - Tech
    - Dev
    - Politics
extra:
  source: https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html
  hostname: www.unixsheikh.com
  author: null
  original_title: The problems with the GPL --- GPL 的问题
  original_lang: en

---

Published on 2021-02-02. Modified on 2022-07-20.  

发布于 2021-02-02。于2022-07-20修改。

In my previous article "Why you should migrate everything from Linux to BSD", in the [License problems](https://www.unixsheikh.com/articles/why-you-should-migrate-everything-from-linux-to-bsd.html#license) section, I very briefly addressed one of the problems with the GPL license. I have since received a few emails asking for elaboration on the subject, which is what I will try to do in this article.  

在我之前的文章“为什么你应该将所有内容从Linux迁移到BSD”中，在许可证问题部分，我非常简要地解决了GPL许可证的一个问题。从那以后，我收到了几封电子邮件，要求详细说明这个主题，这就是我将在本文中尝试做的事情。

### Table of contents 目录

-   [What is the GPL?  
    
    什么是 GPL？](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#what-is-the-gpl)
-   [The GPL encourages "hijacking" and political maneuverings  
    
    GPL鼓励“劫持”和政治操纵](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#hijacking)
-   [The damage done by proprietary companies  
    
    专有公司造成的损害](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#damage)
-   [Not sharing is actually the root of the problem  
    
    不分享其实是问题的根源](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#root-of-the-problem)
-   [The GPL is hypocritical  
    
    GPL是虚伪的](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#hypocritical)
-   [That whole "Linux stealing our code" thing  
    
    整个“Linux窃取我们的代码”的事情](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#deraadt)
-   [The GPL misses the point  
    
    GPL 没有抓住重点](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#gpl-misses-the-point)
-   [Greedy people and political corruption  
    
    贪婪的人和政治腐败](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#greedy-people)
-   [A final comment 结语](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#final-comment)
-   [Further reading 延伸阅读](https://www.unixsheikh.com/articles/the-problems-with-the-gpl.html#further-reading)

## What is the GPL?  

什么是 GPL？

The [GNU Public License (GPL)](https://en.wikipedia.org/wiki/GNU_General_Public_License) was created to be the "antithesis" of the standard proprietary license. Any modifications that were made to GPL licensed software required to be given back to the GPL community and any application that used or linked to GPL source code was required to be under the GPL.  

GNU公共许可证（GPL）被创建为标准专有许可证的“对立面”。对 GPL 许可软件所做的任何修改都需要返回给 GPL 社区，任何使用或链接到 GPL 源代码的应用程序都必须遵循 GPL。

The main purpose of the GPL is to disallow incorporation of GPL licensed software into proprietary software.  

GPL 的主要目的是禁止将 GPL 许可软件合并到专有软件中。

The GPL is rather complex:  

GPL 相当复杂：

-   You cannot sell GPL licensed software, but you can charge as much as you want for distributing, supporting, or documenting the software.  
    
    您不能出售 GPL 许可软件，但您可以为分发、支持或记录软件收取任何费用。
-   If GPL licensed source code is required for a program to compile, the program must also be under the GPL. Linking statically to a GPL library requires a program to be under the GPL.  
    
    如果一个程序需要GPL许可的源代码来编译，那么该程序也必须在GPL下。静态链接到 GPL 库需要程序在 GPL 下。
-   Because the Linux kernel is licensed under the GPL, any code statically linked with the Linux kernel must be GPL licensed itself. This requirement can be avoided by dynamically linking loadable kernel modules. This permits companies to distribute binary drivers, but has the disadvantage that they will only work for a particular versions of the Linux kernel.  
    
    因为 Linux 内核是在 GPL 下授权的，所以任何与 Linux 内核静态链接的代码都必须是 GPL 许可本身。通过动态链接可加载内核模块可以避免此要求。这允许公司分发二进制驱动程序，但缺点是它们仅适用于特定版本的 Linux 内核。

Because of the complexity of the GPL, its legality is mainly being ignored in many parts of the world in regard to Linux and related software.  

由于GPL的复杂性，在世界许多地方，在Linux和相关软件方面，它的合法性主要被忽视。

## The GPL encourages "hijacking" and political maneuverings  

GPL鼓励“劫持”和政治操纵

The GPL and licenses modeled on it impose the restriction that source code must be distributed or made available for all works that are derivatives of the GNU copyrighted code.  

GPL 和以它为蓝本的许可证施加了限制，即源代码必须分发或提供给作为 GNU 版权代码衍生品的所有作品。

While this may look like a noble strategy, it is a condition that is typically unacceptable for commercial use of software. In practice, it usually ends up hindering free sharing and reuse of code and ideas rather than encouraging it.  

虽然这看起来像是一个崇高的策略，但对于软件的商业用途来说，这是一个通常不可接受的条件。在实践中，它通常最终会阻碍代码和想法的自由共享和重用，而不是鼓励它。

One of the problems is that when a company cannot fully control how they share their code, they either don't use the software, or instead try hard to "hijack" the project by political maneuvering, as we have seen with e.g. Red Hat.  

其中一个问题是，当一家公司无法完全控制他们共享代码的方式时，他们要么不使用该软件，要么试图通过政治操纵来“劫持”项目，正如我们在Red Hat中看到的那样。

Pressure to put proprietary applications on Linux became overwhelming in the beginning of 1990. Such applications often must link with system libraries. The pressure was so great that it resulted in a modified version of the GPL called the LGPL ("Library", since renamed to "Lesser", GPL). The LGPL allows proprietary code to be linked to the [GNU C library (glibc)](https://en.wikipedia.org/wiki/GNU_C_Library). You do not have to release the source code which has been dynamically linked to an LGPL licensed library. On the other hand, if you statically link an application with glibc, which is what is very often required in embedded systems, you cannot keep your application proprietary, that is, the source must be released.  

在1990年初，将专有应用程序放在Linux上的压力变得势不可挡。此类应用程序通常必须与系统库链接。压力如此之大，以至于它导致了GPL的修改版本，称为LGPL（“库”，后来更名为“Lesser”，GPL）。LGPL允许专有代码链接到GNU C库（glibc）。您不必发布已动态链接到 LGPL 许可库的源代码。另一方面，如果您将应用程序与 glibc 静态链接（这是嵌入式系统中经常需要的），则无法保持应用程序的专有性，即必须释放源代码。

This kind of restriction sometimes put a company in a sore spot. Instead of releasing source code they try to influence the upstream project by hiring one or more of the developers, and then try to effect the project to make changes upstream that helps the company implement whatever solutions they require. Once this political maneuvering begins it often has very damaging result on the free software community because it doesn't stop there.  

这种限制有时会使公司陷入困境。他们没有发布源代码，而是试图通过雇用一个或多个开发人员来影响上游项目，然后尝试影响项目以在上游进行更改，以帮助公司实施他们需要的任何解决方案。一旦这种政治策略开始，它通常会对自由软件社区产生非常有害的结果，因为它并不止于此。

One such clear example is Red Hat trying hard to get rid of the `/etc` configuration directory on Linux.  

一个这样明显的例子是Red Hat努力摆脱Linux上的 `/etc` 配置目录。

Red Hat wants this change because in their specific business product for the embedded market, `/etc` gets in the way. Having Linux as an operating system not depend upon `/etc` is very important for Red Hat, which is also why they have hardcoded DNS servers from Google, Cloudflare and Quad9 into the systemd-resolved network application, so that it can run completely without any setup in `/etc`. This is also why they are trying to change the way home directories work and systemd-homed is the first major step in that direction. Getting rid of `/etc/passwd` and related files is currently one of the top priority projects at Red Hat as that will enable getting rid of the rest of `/etc` more easily.  

红帽希望做出这种改变，因为在他们针对嵌入式市场的特定业务产品中， `/etc` 阻碍了他们。将Linux作为不依赖 `/etc` 的操作系统对于Red Hat来说非常重要，这也是为什么他们将Google，Cloudflare和Quad9的DNS服务器硬编码到systemd解析的网络应用程序中，以便它可以完全运行 `/etc` 而无需任何设置。这也是为什么他们试图改变主目录的工作方式，systemd-homed是朝着这个方向迈出的第一步。摆脱 `/etc/passwd` 和相关文件目前是红帽的重中之重项目之一，因为这将使摆脱其余 `/etc` 文件更容易。

As a matter of fact, the corporate interests of Red Hat is the very reason behind the existence of systemd in the first place. And it is also the very reason why systemd isn't just an init system, but rather has become a huge pile of interdependent building blocks to make "an operating system" that better serves their interests, both in their embedded market and on the other market shares they have.  

事实上，红帽的企业利益正是systemd存在的原因。这也是为什么systemd不仅仅是一个init系统，而是成为一大堆相互依赖的构建块，以制造“操作系统”，更好地服务于他们的利益，无论是在他们的嵌入式市场还是在他们拥有的其他市场份额。

Red Hat needs these major changes to become an integrated part of the major Linux distributions such that all third party software works on this setup, rather than on the current setup in which Red Hat have to work around a lot of issues, which is both very time consuming and difficult.  

红帽需要这些重大更改才能成为主要Linux发行版的组成部分，以便所有第三方软件都可以在此设置上运行，而不是在当前设置上工作，Red Hat必须解决许多问题，这既非常耗时又困难。

As I have already explained in my article [The real motivation behind systemd](https://unixsheikh.com/articles/the-real-motivation-behind-systemd.html), Red Hat addressed several third party projects and tried to convince them to make their projects depend upon systemd, such as the attempts made by Lennart Poettering on [the Gnome mailing list](https://mail.gnome.org/archives/desktop-devel-list/2011-May/msg00427.html), and the attempt made by Red Hat developer "keszybz" on the [tmux project](https://github.com/tmux/tmux/issues/428). Most of these attempts were disguised as technical issues, however when you read the long email correspondence on the Gnome mailing list and elsewhere, the real intent becomes quite clear.  

正如我已经在我的文章“systemd背后的真正动机”中已经解释的那样，Red Hat讨论了几个第三方项目，并试图说服他们让他们的项目依赖于systemd，例如Lennart Poettering在Gnome邮件列表上的尝试，以及Red Hat开发人员“keszybz”在tmux项目上的尝试。这些尝试中的大多数都伪装成技术问题，但是当您阅读Gnome邮件列表和其他地方的长电子邮件通信时，真正的意图变得非常清晰。

In another example, Red Hat purchased Cygnus, an engineering company that had taken over development of the FSF compiler tools. Cygnus had developed a business model in which they sold support for GNU software. This enabled them to employ some 50 engineers and drive the direction of the programs by contributing the preponderance of modifications.  

在另一个例子中，Red Hat收购了Cygnus，这是一家接管FSF编译器工具开发的工程公司。Cygnus开发了一种商业模式，他们出售对GNU软件的支持。这使他们能够雇用大约50名工程师，并通过贡献大量的修改来推动项目的方向。

While the Linux kernel and Linux distributions used to be mainly community driven projects, the corporate interests of some of the major companies has changed this a lot. Some contributions has benefitted the communities, but a lot of maneuverings has not, and currently Linux, as an operating system (not the kernel alone) is undergoing major changes, changes that reach out far beyond the kernel and the GNU tools.  

虽然Linux内核和Linux发行版过去主要是社区驱动的项目，但一些大公司的企业利益已经改变了很多。一些贡献使社区受益，但很多操作并没有，目前Linux作为一个操作系统（不仅仅是内核）正在经历重大变化，这些变化远远超出了内核和GNU工具。

This kind of "hijacking" and political maneuverings never happen with a permissive license like the BSD or MIT licenses.  

这种“劫持”和政治操纵永远不会发生在像BSD或MIT许可证这样的宽松许可证上。

With a permissive license the company can do whatever they want. The situation never arises in which it becomes a part of their interest to "hijack" the upstream project or directly influence they way it is going.  

有了宽松的许可证，公司可以做任何他们想做的事情。这种情况永远不会出现，即“劫持”上游项目或直接影响他们前进的方式成为他们利益的一部分。

On the contrary, companies who benefit from the permissive license often contribute code back to the project because it is in their interest to have their contributions available in the source code, while at the same time they keep "specific company related" changes private.  

相反，受益于宽松许可证的公司通常会将代码贡献回项目，因为将其贡献在源代码中可用符合他们的利益，同时他们将“特定公司相关”更改保密。

[Clang](https://clang.llvm.org/), which is release under a permissive license, and which originally is a project started at Apple in 2005, is another really good example of the problems with the GPL. GCC is licensed under the terms of the GPL version 3, which requires developers who distribute extensions for, or modified versions of, GCC to make their source code available, whereas LLVM, which is the clang backend, has a BSD-like license that does not have that requirement.  

Clang，它是在宽松许可证下发布的，最初是苹果公司于2005年开始的一个项目，是GPL问题的另一个很好的例子。GCC 根据 GPL 版本 3 的条款获得许可，该版本要求分发 GCC 扩展或修改版本的开发人员提供其源代码，而 LLVM（作为 clang 后端）具有类似 BSD 的许可证，没有该要求。

Because of this Apple chose to develop a new compiler front end from scratch, supporting C, Objective-C and C++. The clang project was then open sourced in 2007 and now contributors who is making improvements and changes to both LLVM and clang includes several of the free software projects such as all the BSD projects, and it also includes major companies like Microsoft, Google, ARM, Sony, Intel and Advanced Micro Devices (AMD).  

正因为如此，苹果选择从头开始开发一个新的编译器前端，支持C，Objective-C和C++。clang项目在2007年开源，现在对LLVM和clang进行改进和更改的贡献者包括几个自由软件项目，如所有的BSD项目，它还包括Microsoft，谷歌，ARM，索尼，英特尔和高级微设备（AMD）等大公司。

Because the GCC source code is a large and difficult system for developers to work with, and because companies often develop specific extensions which they do not want to share, the GCC is now slowly being abandoned, not benefiting from any of the major improvements, and instead a real free alternative is slowly taking its place.  

由于 GCC 源代码对于开发人员来说是一个庞大而难以使用的系统，并且由于公司经常开发他们不想共享的特定扩展，因此 GCC 现在正在慢慢被放弃，没有从任何重大改进中受益，取而代之的是真正的免费替代方案正在慢慢取代它。

## The damage done by proprietary companies  

专有公司造成的损害

Some companies will make improvements which they never share when they build software with a permissive license and they will possibly even make billions of dollars doing it. But this is really not damaging free software in the least.  

一些公司会做出改进，当他们使用宽松许可证构建软件时，他们永远不会分享这些改进，他们甚至可能为此赚取数十亿美元。但这丝毫没有损害自由软件。

What is being damaged is society in general, such as the damage done by Microsoft, Apple and Google with their proprietary spyware operating systems, their copyright licenses and their creepware.  

受到损害的是整个社会，例如Microsoft，苹果和谷歌对其专有间谍软件操作系统，版权许可和蠕变软件造成的损害。

But this damage has absolutely nothing to do with the free software. This damage is the result of the capitalistic political system, and this damage will always exist as long as the political system favors profit over people.  

但这种损害与自由软件完全无关。这种损害是资本主义政治制度的结果，只要政治制度有利于利润而不是人民，这种损害就会永远存在。

And of course the damage that the capitalistic political system is causing is not limited to software or freedom, but extends its greedy reach far into all the other corners of life with devastating consequences as a result. Just look at the current global environment crisis! Or the global rise of extreme poverty! Or the horrifying treatment of animals! All in the name of profit!  

當然，資本主義政治體系造成的破壞不僅限於軟體或自由，而是將其貪婪的影響擴展到生活的所有其他角落，結果帶來了毀滅性的後果。看看当前的全球环境危机就知道了！还是全球极端贫困的崛起！还是对动物的恐怖待遇！一切都以利润的名义！

Whether the GPL or more free software licenses exist or not, this greed and the damage caused by it will always exist. The point is that the GPL doesn't help in the least. The damage will be done regardless of what software licenses are in usage, and it is a problem that needs to be addressed on the political arena, not on the software development arena.  

无论GPL或更多的自由软件许可证是否存在，这种贪婪和由此造成的损害将永远存在。关键是GPL丝毫没有帮助。无论使用什么软件许可证，损害都会造成，这是一个需要在政治舞台上解决的问题，而不是在软件开发领域。

I think it is also worth noting that GPL violations is a widespread problem. All around the world GPL software is treated as "public domain" and the license has very little real impact in many cases. This is why the [The gpl-violations.org project](https://gpl-violations.org/) was created.  

我认为还值得注意的是，违反GPL是一个普遍存在的问题。在世界各地，GPL软件被视为“公共领域”，在许多情况下，许可证几乎没有实际影响。这就是创建 The gpl-violations.org 项目的原因。

The very "soul" of a true free license is encouraging cooperation, it is helping people, and thereby also companies (as they consists of people working together), to see that it doesn't benefit anyone to be greedy, that it is better to share and help each other rather than making single individuals pockets thicker and thicker.  

真正的自由许可证的“灵魂”是鼓励合作，它帮助人们，从而帮助公司（因为它们由一起工作的人组成），看到贪婪对任何人都没有好处，最好是互相分享和帮助，而不是让单个人的口袋越来越厚。

Of course evil individuals will always exist, and some people will never improve, but the fact is that we cannot prevent any damage by the usage of the GPL, what we need to do instead is to educate people so they make better choices. And the politicians need to wake up, their greed and corruption is harming themselves, their own families and the future of their children - nobody is excepted from the exploitation by corporate interests, not even the corrupt politicians themselves.  

当然，邪恶的个人将永远存在，有些人永远不会改善，但事实是我们无法防止使用GPL造成的任何损害，我们需要做的是教育人们，让他们做出更好的选择。政客们需要醒来，他们的贪婪和腐败正在伤害他们自己、他们自己的家庭和他们孩子的未来——没有人能免受企业利益的剥削，即使是腐败的政客本身。

Eventually governments all over the world will be forced to adopt and implement true free software because of the risks involved. **No country can trust software developed in another country unless the source code is fully open and truly free, not even from allied countries! The risk of spying and damage of infrastructure is far too great! Oh, and by the way, that goes for closed hardware as well!**  

最终，由于所涉及的风险，世界各国政府将被迫采用和实施真正的自由软件。任何国家都不能信任在另一个国家开发的软件，除非源代码是完全开放和真正免费的，即使是来自盟国的源代码！间谍和破坏基础设施的风险太大了！哦，顺便说一下，这也适用于封闭硬件！

## Not sharing is actually the root of the problem  

不分享其实是问题的根源

A root cause of evil in the world is poverty. People need to share and help each other, as this will not only eliminate or restrict poverty, but it will also set a precedence in society in which being greedy becomes something very bad.  

世界上邪恶的根源是贫穷。人们需要互相分享和帮助，因为这不仅会消除或限制贫困，而且还会在社会中树立一个先例，在这种先例中，贪婪会变成非常糟糕的事情。

Some people believe that they deserve whatever wealth they have got. They don't want to share, because why should they? They have worked hard to earn their wealth and others can just do the same. But this is wrong.  

有些人认为他们应该得到他们所拥有的任何财富。他们不想分享，因为他们为什么要分享？他们努力工作以赚取财富，其他人也可以这样做。但这是错误的。

Whether you believe in coincidence, luck or God, the fact is that your hard work or clever business strategy is not the cause behind your wealth. Rather it is circumstances far beyond your control. The place you grew up, how you grew up, who your parents where, what people you knew, the opportunities that presented themselves to you as a result of all these different circumstances are in fact all the major factors involved in your success or failure. And none of these things can be attributed to your doing. These things are all far beyond your control. And the fact is that your hard work accounts for almost nothing. You could do even more hard work and even more clever business, but by just moving you a few inches, nothing will turn out the same, and what was a major success in one place, turned out to be a major failure in another place.  

无论你相信巧合、运气还是上帝，事实是你的努力工作或聪明的商业策略并不是你财富背后的原因。相反，这是远远超出你控制范围的情况。你在哪里长大，你如何长大，你的父母在哪里，你认识什么人，由于所有这些不同的情况而呈现给你的机会，实际上是你成功或失败的所有主要因素。这些事情都不能归因于你的行为。这些事情都远远超出你的控制范围。事实是，您的辛勤工作几乎一无所获。你可以做更艰苦的工作，甚至更聪明的生意，但只要移动你几英寸，一切都不会一样，在一个地方取得重大成功的东西，在另一个地方却是重大失败。

And these things are the very reason why you need to share, whether it is software or wealth. Because none of these circumstances has anything to do with you, your wealth is not something you have accumulated by genius on your part, not by a long shot, and by not helping other people, and by keeping wealth out of the hands of others and into your own pockets, you're setting a really bad example for others, which is the most damaging part of all of this. **By not sharing you are showing the youth and other people that in order to be rich and wealthy, they need to be like you!** And this results in less people sharing, less people helping each other, and absolutely nothing is more damaging to our human race as a whole than greed.  

这些东西正是你需要分享的原因，无论是软件还是财富。因为这些情况都与你无关，你的财富不是你天才积累的，不是靠远射，不是靠不帮助别人，把财富从别人手中拿进自己的口袋里，你正在为别人树立一个非常糟糕的榜样， 这是所有这一切中最具破坏性的部分。通过不分享你，你向年轻人和其他人表明，为了变得富有和富有，他们需要像你一样！这导致更少的人分享，更少的人互相帮助，绝对没有什么比贪婪对我们整个人类的伤害更大了。

By sharing and helping we encourage good behavior and good relations and if only a majority of us keep doing that, at one point "being evil" will not only not pay off, but it will be so damaging to the end result that you simply must refrain.  

通过分享和帮助我们鼓励良好的行为和良好的关系，如果我们中的大多数人继续这样做，那么在某一时刻，“作恶”不仅不会得到回报，而且会对最终结果造成如此大的损害，以至于你必须克制。

We do not prevent evil in the software world, or in the world generally, by using the GPL. Companies like Microsoft will do evil no matter what. They will make they own software no matter what. Preventing them from using your specific software doesn't change anything and it actually often does more damage than good. But by doing good on a large scale and by educating people, the end result will be that nobody will buy anything from an evil company.  

我们不能通过使用GPL来防止软件世界或整个世界的邪恶。像Microsoft这样的公司无论如何都会作恶。无论如何，他们都会让自己拥有自己的软件。阻止他们使用您的特定软件不会改变任何东西，实际上它通常弊大于利。但是，通过大规模做好事和教育人们，最终结果将是没有人会从邪恶的公司购买任何东西。

Currently only few people understand this and few projects work like this, which is why it is such a slow going process. But the GPL is not helping at all, it is making things worth when greedy companies "hijack" projects. Just look at the damage the corporate interest in systemd has caused to something like the Debian project, just as an example.  

目前只有很少有人理解这一点，很少有项目像这样工作，这就是为什么这是一个如此缓慢的过程。但是GPL根本没有帮助，当贪婪的公司“劫持”项目时，它使事情变得值得。举个例子，企业对systemd的兴趣对Debian项目造成了多大的损害。

## The GPL is hypocritical  

GPL是虚伪的

As we all know the [GNU project](https://www.gnu.org/) and the [Free Software Foundation](https://www.fsf.org/) is doing a lot of work to promote Free Software. On the FSF website we find the [following definition](https://www.gnu.org/philosophy/free-sw.html) on "free software":  

众所周知，GNU工程和自由软件基金会正在做大量的工作来推广自由软件。在 FSF 网站上，我们找到了以下关于“自由软件”的定义：

> "Free software" means software that respects users' freedom and community. Roughly, it means that the users have the freedom to run, copy, distribute, study, change and improve the software. Thus, "free software" is a matter of liberty, not price. To understand the concept, you should think of "free" as in "free speech," not as in "free beer". We sometimes call it "libre software," borrowing the French or Spanish word for "free" as in freedom, to show we do not mean the software is gratis.  
> 
> “自由软件”是指尊重用户自由和社区的软件。粗略地说，这意味着用户可以自由运行，复制，分发，研究，更改和改进软件。因此，“自由软件”是一个自由问题，而不是价格问题。要理解这个概念，你应该把“自由”想象成“言论自由”，而不是“免费啤酒”。我们有时称它为“自由软件”，借用法语或西班牙语中的“自由”一词，以表明我们并不意味着该软件是免费的。
> 
> We campaign for these freedoms because everyone deserves them. With these freedoms, the users (both individually and collectively) control the program and what it does for them. When users don't control the program, we call it a "nonfree" or "proprietary" program.
> 
>   
> 
> 我们为这些自由而奔走，因为每个人都应得这些自由。有了这些自由，用户（个人和集体）控制程序以及它为他们做什么。当用户不控制程序时，我们称之为“非自由”或“专有”程序。

At the same time the GNU project and FSF endorses and make heavy use of the [GPL](https://en.wikipedia.org/wiki/GNU_General_Public_License), which by its very nature is "nonfree", according to this very definition put forward in the above, because it restricts what you can do with the software. I am not talking about a philosophical discussion about freedom, or that true freedom is about being able to act without restrictions, that's not what this is about. It's about the fact that the GPL is contradicting the very purpose for which it was created.  

同时，GNU工程和FSF认可并大量使用GPL，根据上面提出的这个定义，GPL本质上是“非自由的”，因为它限制了你可以用软件做什么。我不是在谈论关于自由的哲学讨论，或者真正的自由是关于能够不受限制地行动，这不是关于这个目的。这是关于GPL与创建它的目的相矛盾的事实。

The very restrictions set up by the GPL is in essence nonfreedom, and this is not from a philosophical perspective, but from a true implementation perspective. The GPL is at the very root cause at why many open source projects released by a permissive license cannot be integrated into Linux.  

GPL设置的限制本质上是非自由的，这不是从哲学的角度，而是从真正的实现角度。GPL是为什么许多由宽松许可证发布的开源项目不能集成到Linux中的根本原因。

This is contrary to a [permissive license](https://en.wikipedia.org/wiki/Permissive_software_license) and e.g. on the [OpenBSD's goals website](https://www.openbsd.org/goals.html) it states:  

这与宽松的许可证相反，例如在OpenBSD的目标网站上，它指出：

> We want to make available source code that anyone can use for ANY PURPOSE, with no restrictions. We strive to make our software robust and secure, and encourage companies to use whichever pieces they want to.  
> 
> 我们希望提供任何人都可以用于任何目的的源代码，没有任何限制。我们努力使我们的软件强大而安全，并鼓励公司使用他们想要的任何部分。

## That whole "Linux stealing our code" thing  

整个“Linux窃取我们的代码”的事情

Below I will post the email that [Theo de Raadt](https://en.wikipedia.org/wiki/Theo_de_Raadt), the founder of the [OpenBSD](https://www.openbsd.org/) project [wrote](https://marc.info/?l=openbsd-misc&m=118861134304239&w=2) in August 2007, when a group of Linux developers attempted to modify the license of dual-licensed ath5k driver.  

下面我将发布OpenBSD项目的创始人Theo de Raadt在2007年8月写的电子邮件，当时一群Linux开发人员试图修改双许可ath5k驱动程序的许可证。

```
I stopped making public statements in the recent controversy because Eben Moglen started working behind the scenes to 'improve' what Linux people are doing wrong with licensing, and he asked me to give him pause, so his team could work.  Honestly, I was greatly troubled by the situation, because even people like Alan Cox were giving other Linux developers advice to ... break the law.  And furthermore, there are even greater potential risks for how the various communities interact.

For the record -- I was right and the Linux developers cannot change the licenses in any of those ways proposed in those diffs, or that conversation (http://lkml.org/lkml/2007/8/28/157).

It is illegal to modify a license unless you are the owner/author, because it is a legal document.  If there are multiple owners/authors, they must all agree.  A person who receives the file under two licenses can use the file in either way....  but if they distribute the file (modified or unmodified!), they must distribute it with the existing license intact, because the licenses we all use have statements which say that the license may not be removed.

It may seem that the licenses let one _distribute_ it under either license, but this interpretation of the license is false -- it is still illegal to break up, cut up, or modify someone else's legal document, and, it cannot be replaced by another license because it may not be removed.  Hence, a dual licensed file always remains dual licensed, every time it is distributed.

Now I've been nice enough to give Eben and his team a few days time to communicate inside the Linux community, to convince them that what they have proposed/discussed is wrong at a legal level.  I think that Eben also agrees with me that there are grave concerns about how this leads to problems at the ethical and community levels (at some level, a ethos is needed for Linux developers to work with *BSD developers). And there are possibilities that similar issues could loom in the larger open source communities who are writing applications.

Eben has thus far chosen not to make a public statement, but since time is running out on people's memory, I am making one.  Also, I feel that a lot of Linux "relicencing" meme-talkin' trolls basically have attacked me very unfairly again, so I am not going to wait for Eben to say something public about this.

In http://lkml.org/lkml/2007/8/29/183, Alan Cox managed to summarize what Jiri Slaby and Luis Rodriguez were trying to do by proposing a modification of a Dual Licenced file without the consent of all the authors.  Alan asks "So whats the problem ?".  Well, Alan, I must caution you -- your post is advising people to break the law.

I will attempt to describe in simple terms, based on what I have been taught, how one must handle such licenses:

- If you receive dual licensed code, you may not delete the license you don't like and then distribute it.  It has to stay, because you may not edit someone's else's license -- which is a three-part legal document (For instance: Copyright notice, BSD, followed by GPL).

- If you receive ISC or BSD licensed code, you may not delete the license. Same principle, since the notice says so. It's the law. Really.

- If you add "large pieces of originality" to the code which are valid for copyright protection on their own, you may choose to put a different and seperate (must be non-conflicting...) license at the top of the file above the existing license.

    (Warning: things become less clear as to what the combination of licenses mean, though -- there are ethical traps, too).

- If you wish for everyone to remain friends, you should give code back.

  That means (at some ethical or friendliness level) you probably do not want to put a GPL at the top of a BSD or ISC file, because you would be telling the people who wrote the BSD or ISC file:

     "Thanks for what you wrote, but this is a one-way street, you give us code, and we take it, we give you you nothing back. screw off."

In either case, I think a valuable lessons has been taught us here in the BSD world -- there are many many GPL loving people who are going to try to find any way to not give back and share (I will mention one name: Luis Rodriguez has been a fanatic pushing us for dual licensed, and I feel he is to blame for this particular problem).  Many of those same people have been saying for years that BSD code can be stolen, and that is why people should GPL their code.

Well, the lesson they have really taught us is that they consider the GPL their best tool to take from us!

GPL fans said the great problem we would face is that companies would take our BSD code, modify it, and not give back.  Nope -- the great problem we face is that people would wrap the GPL around our code, and lock us out in the same way that these supposed companies would lock us out.  Just like the Linux community, we have many companies giving us code back, all the time.  But once the code is GPL'd, we cannot get it back.

Ironic.

I hope some people in the GPL community will give that some thought. Your license may benefit you, but you could lose friends you need. The GPL users have an opportunity to 'develop community', to keep an ethic of sharing alive.

If the Linux developers wrap GPL's around things we worked very hard on, it will definately not be viewed as community development.

Thank you for thinking about this.

[I ask that one person make sure that one copy of this ends up on the linux kernel mailing list]

```

## The GPL misses the point  

GPL 没有抓住重点

When people use the GPL they mostly try to prevent some corporate entity from taking their software, make improvements or changes to it, and then sell that software as a proprietary product.  

当人们使用GPL时，他们大多试图阻止一些公司实体拿走他们的软件，对其进行改进或更改，然后将该软件作为专有产品出售。

But what is it that we're trying to accomplish? Is it competition by proprietary software? Is it to prevent people from making money by developing software and getting food on the table?  

但是我们要实现什么？是专有软件的竞争吗？是为了防止人们通过开发软件和在餐桌上获得食物来赚钱吗？

Let's quote Richard Stallman:  

让我们引用理查德·斯托曼的话：

> To use free software is to make a political and ethical choice asserting the right to learn, and share what we learn with others. Free software has become the foundation of a learning society where we share our knowledge in a way that others can build upon and enjoy.  
> 
> 使用自由软件就是做出政治和道德选择，主张学习的权利，并与他人分享我们学到的东西。自由软件已经成为一个学习型社会的基础，在这个社会中，我们以一种其他人可以建立和享受的方式分享我们的知识。
> 
> Currently, many people use proprietary software that denies users these freedoms and benefits. If we make a copy and give it to a friend, if we try to figure out how the program works, if we put a copy on more than one of our own computers in our own home, we could be caught and fined or put in jail. That's what's in the fine print of the license agreement you accept when using proprietary software.
> 
>   
> 
> 目前，许多人使用专有软件剥夺了用户的这些自由和好处。如果我们制作一份副本并交给朋友，如果我们试图弄清楚该程序是如何工作的，如果我们在自己家中的多台计算机上放置一份副本，我们可能会被抓到罚款或入狱。这就是您在使用专有软件时接受的许可协议细则中的内容。

This is a highly convoluted explanation with several contradictions.  

这是一个高度复杂的解释，有几个矛盾。

I say: Don't use proprietary software that prevents you from giving a friend a copy. Don't use proprietary software that spies on you or limits your usage of your hardware. Educate the masses to use true free software, but don't be hypocritical by arguing against freedom limiting licensees, and then at the same restrict true software freedom.  

我说：不要使用阻止你给朋友副本的专有软件。不要使用监视您或限制您使用硬件的专有软件。教育大众使用真正的自由软件，但不要虚伪地反对限制自由的被许可者，同时限制真正的软件自由。

## Greedy people and political corruption  

贪婪的人和政治腐败

I think we can all agree that there is nothing wrong with people building software to make a living and putting food on the table for their families. What we don't like is when people, and thereby companies, becomes too greedy.  

我想我们都同意，人们为了谋生而构建软件并为家人提供食物并没有错。我们不喜欢的是人们，从而公司，变得过于贪婪。

In 1969 (what I like to call a corrupt) US Department of Justice, charged IBM with destroying businesses by bundling free software with IBM hardware. The result of this was that IBM unbundled its software from their hardware and software became independent products separate from hardware. In 1968 a company called Informatics introduced the first commercial software application and managed to established the concept of "the software product" and very high rates of return. Informatics developed the perpetual license, which is now standard throughout the computer industry, wherein ownership is never transferred to the customer.  

1969年（我喜欢称之为腐败的）美国司法部指控IBM通过将自由软件与IBM硬件捆绑在一起来摧毁企业。这样做的结果是IBM将其软件从他们的硬件中分离出来，软件成为独立于硬件的独立产品。1968年，一家名为Informatics的公司推出了第一个商业软件应用程序，并设法建立了“软件产品”的概念和非常高的回报率。Informatics开发了永久许可证，现在已成为整个计算机行业的标准，其中所有权永远不会转让给客户。

This is the problem at heart - greed!  

这就是核心问题——贪婪！

It goes against the very foundation of rationality to even think the idea that when you purchase something, it still doesn't belong to you. It is so self-contradictory that nobody in their right mind can accept this nonsense, and it truly requires corruption at the highest level to accept such crap and enforce it by law! This is also why so-called software piracy will never ever be stopped. It is in the nature of man to share and help his fellow man! Only the most greedy and corrupt person is against this.  

甚至认为当你购买某样东西时，它仍然不属于你的想法是违背理性的基础的。这是如此自相矛盾，没有一个头脑正常的人可以接受这种胡说八道，它确实需要最高级别的腐败来接受这种废话并依法执行！这也是为什么所谓的软件盗版永远不会停止的原因。分享和帮助他的同胞是人的天性！只有最贪婪和腐败的人才会反对这一点。

And this is the very core problem with capitalism, it is solely driven by financial interests!  

这是资本主义的核心问题，它完全是由经济利益驱动的！

While we could say that the GPL is created on the premise that people are generally selfish and evil, and will never contribute back unless forced to, it doesn't solve the problem and it doesn't help. What we need is a license that operates on the premise that people are generally decent, and that many will contribute back on principle and goodness. Then we need to educate and set good examples, avoid and shun greed, and I strongly believe we will get the best results by using a more permissive license than the GPL.  

虽然我们可以说GPL是在人们通常是自私和邪恶的前提下创建的，除非被迫，否则永远不会回馈，但它不能解决问题，也没有帮助。我们需要的是一个许可证，其运作前提是人们通常是体面的，并且许多人会根据原则和善良做出贡献。然后我们需要教育和树立好榜样，避免和避免贪婪，我坚信使用比GPL更宽松的许可证会得到最好的结果。

Just as a final comment. I understand the historical background and why the GPL was made and I truly and deeply respect the reasons behind the GPL. And it's not that I believe that the GPL is evil, it's just that I don't believe it is achieving the goals today which it was set out to achieve. I believe it is causing more harm than good in todays software world. I also don't believe that you can encourage freedom and sharing by enforcing nonfreedom, it is a double standard no matter how you look at it.  

作为最后的评论。我了解 GPL 的历史背景和原因，我真诚而深刻地尊重 GPL 背后的原因。这并不是说我相信GPL是邪恶的，只是我不相信它今天实现了它所要实现的目标。我相信它在当今的软件世界中弊大于利。我也不相信你可以通过执行非自由来鼓励自由和分享，无论你怎么看，这都是双重标准。

We also have to remember and put a focus on the fact that corporations consists of people, mainly people trying to get food on the table. We're only truly dealing with people, not software.  

我们还必须记住并关注这样一个事实，即公司由人组成，主要是试图将食物放在餐桌上的人。我们真正与人打交道，而不是软件。

I also believe that some of the views of Richard Stallman are extreme and misguided, and that you will never reach people by preaching a douple standard.  

我也相信理查德·斯托曼的一些观点是极端和误导的，你永远不会通过宣扬双重标准来接触人们。

I believe that we can put greedy and extreme companies on the one side, and Richard Stallman and extreme anti-corporate organizations on the other. Neither of these extremes truly benefit us in any way.  

我相信我们可以把贪婪和极端的公司放在一边，把理查德·斯托曼和极端的反企业组织放在另一边。这两种极端都没有真正使我们受益。

## Further reading 延伸阅读

-   [That whole "Linux stealing our code" thing  
    
    整个“Linux窃取我们的代码”的事情](https://marc.info/?l=openbsd-misc&m=118861134304239&w=2)
-   [History of free and open-source software  
    
    自由和开源软件的历史](https://en.wikipedia.org/wiki/History_of_free_and_open-source_software)
-   [Why you should use a BSD style license for your Open Source Project  
    
    为什么你应该在开源项目中使用 BSD 风格的许可证](https://docs.freebsd.org/en/articles/bsdl-gpl/article.html)
-   [The Free-Libre / Open Source Software (FLOSS) License Slide  
    
    自由/开源软件 （FLOSS） 许可证幻灯片](https://dwheeler.com/essays/floss-license-slide.html)
-   [Open Source Licenses by Category  
    
    按类别划分的开源许可证](https://opensource.org/licenses/category)
-   [Real men don't attack straw men](https://marc.info/?l=openbsd-misc&m=119730630513821&w=2) (the whole thread is relevant, but especially the - straight to the point - responses by Theo de Raadt to Richard Stallman, such as [this](https://marc.info/?l=openbsd-misc&m=119750352332512&w=2), [this](https://marc.info/?l=openbsd-misc&m=119750526002139&w=2), [this](https://marc.info/?l=openbsd-misc&m=119757477532409&w=2), [this](https://marc.info/?l=openbsd-misc&m=119757768504969&w=2) and [this](https://marc.info/?l=openbsd-misc&m=119758183611637&w=2))  
    
    真正的男人不会攻击稻草人（整个线程是相关的，但尤其是 - 直截了当 - 西奥·德·拉德特对理查德·斯托曼的回应，比如这个，这个，这个，这个和这个）
-   [The mysterious history of the MIT License  
    
    麻省理工学院执照的神秘历史](https://opensource.com/article/19/4/history-mit-license)
-   [GPL Violations 违反 GPL 的行为](https://gpl-violations.org/)
