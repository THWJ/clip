---
title: 我们应该聊天吗？微信生态系统中的隐私
date: 2024-01-05T08:08:25.000Z
updated: 2024-01-05T08:08:25.000Z
taxonomies:
  tags:
    - Tech
    - Politics
    - China
extra:
  source: https://citizenlab.ca/2023/06/privacy-in-the-wechat-ecosystem-full-report/
  hostname: citizenlab.ca
  author: Mona Wang
  original_title: Should We Chat? Privacy in the WeChat Ecosystem - The Citizen Lab
  original_lang: en

---

[](https://citizenlab.ca/category/research/)[Research](https://citizenlab.ca/category/research/)[App Privacy and Controls](https://citizenlab.ca/category/research/app-privacy-and-security/)

June 28, 2023  

作者：Mona Wang、Pellaeon Lin 和 Jeffrey Knockel2023 年 6 月 28 日

This report is part one of a two-part series on a privacy and security analysis of the WeChat ecosystem. We’ve created an [FAQ to accompany this report](https://citizenlab.ca/2023/06/privacy-in-the-wechat-ecosystem-explained/ "Privacy in WeChat FAQ").  

本报告是关于微信生态系统隐私和安全分析的两部分系列报告的第一部分。我们创建了一个常见问题解答来配合此报告。

## Key findings 主要发现

-   This work performs the first analysis of WeChat’s tracking ecosystem. Using reverse engineering methods to intercept WeChat’s network requests, we identified exactly what types of data the WeChat app is sending to its servers, and when.  
    
    这项工作对微信的跟踪生态系统进行了首次分析。使用逆向工程方法来拦截微信的网络请求，我们准确地确定了微信应用程序向其服务器发送的数据类型以及时间。
-   During usage of core WeChat features, such as Messaging or Moments, network requests generally contained data that was necessary for the function of the application, and not significantly more; this is in keeping with the WeChat privacy policy for non-mainland-Chinese phone numbers.  
    
    在使用微信核心功能（如消息或朋友圈）期间，网络请求通常包含应用程序功能所需的数据，而不是更多;这符合微信对非中国大陆电话号码的隐私政策。
-   We found that the most fine-grained activity tracking data is sent during Mini Program execution. All Mini Programs, and thereby their users, are enrolled in usage tracking, meaning that a large amount of users’ activity in the Mini Program is sent to WeChat and not just the Mini Program developers themselves.  
    
    我们发现，最细粒度的活动跟踪数据是在小程序执行过程中发送的。所有小程序及其用户都注册了使用跟踪，这意味着用户在小程序中的大量活动被发送到微信，而不仅仅是小程序开发者自己。
-   Permission boundaries between Mini Programs and the host WeChat platform are unclear. As one consequence, we found that granting permissions such as location permission during the use of a Mini Program will also enable the larger transmission of geolocation data to WeChat.  
    
    小程序与主方微信平台之间的权限边界不明确。因此，我们发现，在使用小程序时授予位置权限等权限，也可以实现更大规模的地理位置数据传输到微信。
-   We identify disclosure gaps with WeChat’s privacy policy, which implies that only third-parties collect usage data related to Mini Programs, when, in fact, WeChat also collects this data.  
    
    我们发现 WeChat 的隐私政策存在披露漏洞，这意味着只有第三方收集与小程序相关的使用数据，而实际上，WeChat 也收集这些数据。
-   Some important features within WeChat, such as Advanced Search and Channels, are not governed by WeChat’s own Privacy Policy. Instead, they are governed by Weixin’s Privacy Protection Guidelines. The WeChat Privacy Policy states that these “third-party” services are “operated by Weixin.” Usually, the Weixin Privacy Protection Guidelines apply in whole to users signing up with Chinese phone numbers. Because of this, a user’s data might be subjected to a worse protection than the user thinks.  
    
    WeChat 中的一些重要功能，例如高级搜索和频道，不受 WeChat 自己的隐私政策的约束。相反，它们受微信隐私保护指南的约束。微信隐私政策指出，这些“第三方”服务“由微信运营”。通常，《微信隐私保护指南》完全适用于使用中国电话号码注册的用户。因此，用户的数据可能受到比用户想象的更糟糕的保护。

## Introduction 介绍

With over [1.2 billion monthly active users](https://www.messengerpeople.com/global-messenger-usage-statistics), WeChat is the most popular messaging and social media platform in China and third in the world. According to some market research, network traffic from WeChat [made up 34%](https://walkthechat.com/wechat-impact-report-2016/) of Chinese mobile traffic in 2018. WeChat has in many ways monopolized messaging in China, making it necessary for individuals in China to use. WeChat has also evolved beyond simply messaging. People commonly use WeChat as a social media platform to share updates with contacts, as a platform for conducting financial transactions, and also as a platform for downloading and using other programs, referred to as “Mini Programs.”  

微信拥有超过 12 亿月活跃用户，是中国最受欢迎的消息传递和社交媒体平台，也是全球第三大平台。根据一些市场研究，2018年来自微信的网络流量占中国移动流量的34%。微信在许多方面垄断了中国的消息传递，这使得中国的个人有必要使用。微信也已经超越了简单的消息传递。人们通常将微信用作与联系人分享更新的社交媒体平台，作为进行金融交易的平台，以及作为下载和使用其他程序的平台，称为“小程序”。

WeChat has not only become the default way to contact people in China, but its ecosystem also encompasses many other necessities of daily life, like performing financial transactions or calling taxis. Many inside and outside China, therefore, use WeChat out of necessity. Besides individuals in China, diaspora populations, family members, journalists, international activists, diplomats, people who do business in China, and just about anyone with a relationship in China also use WeChat out of necessity. WeChat also complies with [Chinese government](https://www.wired.com/story/inside-chinas-massive-surveillance-operation/) and [local police](https://www.wsj.com/articles/jailed-for-a-text-chinas-censors-are-spying-on-mobile-chat-groups-1512665007) [requests](https://www.sixthtone.com/news/1003073) for data and information, essentially becoming a mass surveillance tool for local authorities. It also operates a massive [content](https://citizenlab.ca/2015/07/tracking-censorship-on-wechat-public-accounts-platform/) [censorship](https://citizenlab.ca/2017/04/we-cant-chat-709-crackdown-discussions-blocked-on-weibo-and-wechat/) [ecosystem](https://citizenlab.ca/2018/08/cant-picture-this-an-analysis-of-image-filtering-on-wechat-moments/) for the features on its platform.  

微信不仅已成为中国人联系的默认方式，而且其生态系统还包含许多其他日常生活必需品，例如进行金融交易或叫出租车。因此，中国国内外的许多人出于必要而使用微信。除了在中国的个人，侨民、家庭成员、记者、国际活动家、外交官、在中国做生意的人，以及几乎任何在中国有关系的人，也出于必要而使用微信。微信还符合中国政府和地方警方对数据和信息的要求，实质上成为地方当局的大规模监控工具。它还为其平台上的功能运营着一个庞大的内容审查生态系统。

Understanding what data the WeChat application and ecosystem transmits, and to whom, may be especially important due to the heavily automated surveillance and content censorship ecosystem operated by the platform. For vulnerable populations that must use WeChat (for instance, domestic journalists and foreign correspondents, grassroots and diaspora activists), knowing the limitations of the app can protect them. This kind of risk assessment requires a more granular understanding of information flows within the WeChat ecosystem.  

了解微信应用程序和生态系统传输哪些数据以及传输给谁，可能尤为重要，因为该平台运营着高度自动化的监控和内容审查生态系统。对于必须使用微信的弱势群体（例如，国内记者和外国记者、草根和侨民活动家），了解该应用程序的局限性可以保护他们。这种风险评估需要对微信生态系统内的信息流有更细致的了解。

In the case of WeChat, a large portion of network communications, including when messaging, viewing WeChat’s “Moments” posts, or sometimes even when using WeChat Mini Programs, utilize a proprietary encryption protocol called MMTLS. The closed-source and undocumented nature of this network protocol has also made it difficult for researchers to conduct a thorough review of information flows from the application. In our study we had to develop our own tools to enable us to thoroughly study the information that flows back to WeChat servers.  

就微信而言，大部分网络通信，包括消息传递、查看微信的“朋友圈”帖子，有时甚至使用微信小程序时，都使用一种称为 MMTLS 的专有加密协议。该网络协议的闭源和无文档性质也使研究人员难以对来自应用程序的信息流进行彻底审查。在我们的研究中，我们必须开发自己的工具，使我们能够彻底研究流回微信服务器的信息。

Our primary research question investigates what information flows back to WeChat servers across the WeChat ecosystem. To set the stage for this work, we first reverse engineer the networking stack in order to develop instrumentation and tooling to study WeChat network requests. In a follow-up report, we will further discuss our full understanding of the network stack, including the custom network security measures employed by WeChat to encrypt message data.  

我们的主要研究问题调查了整个微信生态系统中哪些信息流回微信服务器。为了给这项工作奠定基础，我们首先对网络堆栈进行逆向工程，以开发用于研究微信网络请求的仪器和工具。在后续报告中，我们将进一步讨论我们对网络堆栈的充分理解，包括微信用于加密消息数据的自定义网络安全措施。

We then use this tooling to systematically categorize and study the composition of network requests flowing from the WeChat client to the server in various contexts in the WeChat ecosystem.  

然后，我们利用这个工具对微信生态系统中各种情况下从微信客户端流向服务器的网络请求的构成进行系统分类和研究。

## Background 背景

WeChat is often described as a “[super-app](https://en.wikipedia.org/wiki/Super-app)” not only due to the large number of features which it has accrued since its inception, but also because it is a popular platform for third-party applications. Originally developed as a chat app, the WeChat platform has grown to support voice calls, “Moments” social media posts, and file sharing. Specific to China, the app also serves as a major payment and financial transaction platform. Globally, the app also supports Mini Programs, which are a key feature relied on by a majority of WeChat users.  

微信经常被描述为“超级应用程序”，不仅因为它自成立以来积累了大量功能，还因为它是第三方应用程序的流行平台。微信平台最初是作为聊天应用程序开发的，现在已经发展到支持语音通话、“朋友圈”社交媒体帖子和文件共享。具体到中国，该应用程序也是一个主要的支付和金融交易平台。在全球范围内，该应用程序还支持小程序，这是大多数微信用户依赖的关键功能。

Despite WeChat’s global popularity, the platform has come under repeated scrutiny for security and privacy issues. The platform lacks end-to-end encryption of chat messages, giving Tencent visibility into all messages sent over the platform. Users with mainland China accounts are subjected to [automated, keyword-based censorship](https://citizenlab.ca/2016/11/wechat-china-censorship-one-app-two-systems/) of messages, and images they [post](https://citizenlab.ca/2018/08/cant-picture-this-an-analysis-of-image-filtering-on-wechat-moments/) or [send via chat message](https://citizenlab.ca/2019/07/cant-picture-this-2-an-analysis-of-wechats-realtime-image-filtering-in-chats/) are censored according to the text contained in those images and according to their similarity to images on an internal blacklist. While such censorship is commonly believed to only affect users with mainland China accounts, previous work has found how [even the communications of non-China users](https://citizenlab.ca/2020/05/we-chat-they-watch/) are subjected to political surveillance and used to build up WeChat’s Chinese political censorship system.  

尽管微信在全球很受欢迎，但该平台因安全和隐私问题而一再受到审查。该平台缺乏对聊天消息的端到端加密，使腾讯能够查看通过该平台发送的所有消息。拥有中国大陆帐户的用户将受到基于关键字的自动消息审查，他们通过聊天消息发布或发送的图像会根据这些图像中包含的文本以及它们与内部黑名单上的图像的相似性进行审查。虽然人们普遍认为这种审查只影响拥有中国大陆账户的用户，但以前的研究发现，即使是非中国用户的通信也受到政治监视，并被用来建立微信的中国政治审查系统。

### What are Mini Programs and why are they important?  

什么是小程序，为什么它们很重要？

Mini Programs are lightweight applications that can be downloaded and launched within the WeChat program, and can also sync and link with users’ WeChat account and certain associated data, like their contact information. The breadth and variety of Mini Programs is essentially the same as any other application ecosystem, covering e-commerce, health, public services, gaming, and any other service you could feasibly imagine an app would be used for. Some Mini Programs deal with particularly sensitive data, such as health apps (e.g. Tencent Health), government service apps (e.g., the [local contact tracing apps](https://www.sixthtone.com/news/1005452) that were compulsory during the COVID-19 pandemic), or apps that perform financial transactions on behalf of the user (e.g., shopping apps like Pinduoduo or budgeting apps like [“Small Ledger”/收款小账本](https://wx.gtimg.com/payapp/md_h5/static/xzb.html)).  

小程序是轻量级的应用程序，可以在微信程序中下载和启动，还可以与用户的微信帐户和某些相关数据（如他们的联系信息）同步和链接。小程序的广度和种类与任何其他应用程序生态系统基本相同，涵盖电子商务、健康、公共服务、游戏以及您可以想象应用程序将用于的任何其他服务。一些小程序处理特别敏感的数据，例如健康应用程序（例如腾讯健康）、政府服务应用程序（例如，在 COVID-19 大流行期间强制使用的本地接触者追踪应用程序）或代表用户进行金融交易的应用程序（例如，拼多多等购物应用程序或“小账本”/收款小账本等预算应用程序）。

WeChat implements Mini Programs by loading web pages into an embedded browser instance. Mini Program developers, then, can provide WeChat a package much like a website that includes HTML-like, Javascript, and CSS files to load into the embedded browser. WeChat also injects JavaScript into the web page. Among other purposes, some of these injected scripts provide a Javascript interface (under namespace “wx”). This interface allows the web-based Mini Program access to various Operating System-level features, like geolocation, with WeChat acting as a bridge between the two. The interface also allows the Mini Program to access data associated with the user’s WeChat account, such as payment information or the user’s phone number.  

微信通过将网页加载到嵌入式浏览器实例中来实现小程序。然后，小程序开发人员可以为微信提供一个包，就像一个网站一样，其中包含类似 HTML、Javascript 和 CSS 的文件，可以加载到嵌入式浏览器中。微信还将 JavaScript 注入到网页中。除其他目的外，其中一些注入的脚本提供了一个 Javascript 接口（在命名空间“wx”下）。该接口允许基于 Web 的小程序访问各种操作系统级别的功能，例如地理位置，微信充当两者之间的桥梁。该接口还允许小程序访问与用户微信账号关联的数据，例如支付信息或用户的电话号码。

The Mini Program ecosystem has also undergone criticism around various privacy and security issues. A [2020 report from CNCERT/CC](https://www.cert.org.cn/publish/main/upload/File/2020%20Annual%20Report.pdf) found that 60 percent of the 50 banking applications that they investigated did not encrypt any user data transmitted over the network, among a litany of other common security issues. [Another report](https://www.sixthtone.com/news/1006196) investigated the third-party tracking ecosystem across 52 commonly used Mini Programs, found that many shared user data with third parties, and generally provided unsatisfactory notice and opt-outs to users.  

小程序生态也因各种隐私和安全问题而受到批评。CNCERT/CC 2020 年的一份报告发现，在他们调查的 50 个银行应用程序中，有 60% 没有加密通过网络传输的任何用户数据，以及一连串其他常见的安全问题。另一份报告调查了 52 个常用小程序的第三方跟踪生态系统，发现许多小程序与第三方共享用户数据，并且通常向用户提供不满意的通知和选择退出。

Since the CNCERT report, WeChat has attempted to [tighten user data controls](https://www.scmp.com/tech/apps-social/article/3065206/tencents-wechat-tightens-privacy-controls-third-party-apps-calls) within its Mini Program ecosystem. One such example is that web requests can no longer be directly made from the Mini Program, and instead must go through WeChat’s internal API. This way, WeChat can enforce which third-parties are contacted during Mini Program usage, and also enforce minimum security for network requests, in particular by ensuring that they are all encrypted using HTTPS.  

自CNCERT发布报告以来，微信一直试图在其小程序生态系统中加强用户数据控制。一个这样的例子是，Web 请求不能再直接从小程序发出，而是必须通过微信的内部 API。这样一来，微信就可以强制要求在小程序使用过程中联系哪些第三方，也可以对网络请求强制执行最低安全性，特别是确保它们都使用HTTPS加密。

Even though WeChat and Mini Programs are popular, data transmission and information flow across these third-party ecosystems is understudied when compared to [Android](https://ieeexplore.ieee.org/abstract/document/8660581) and [iOS](https://www.ndss-symposium.org/wp-content/uploads/2017/09/egel.pdf). Previous work has attempted to use automated methods to [analyze the Windows desktop version](https://dl.acm.org/doi/pdf/10.1145/3193111.3193114) of WeChat, finding that various identifiers related to a user’s machine are transmitted to WeChat’s servers.  

尽管微信和小程序很受欢迎，但与 Android 和 iOS 相比，这些第三方生态系统中的数据传输和信息流研究不足。之前的工作曾尝试使用自动化方法来分析微信的Windows桌面版本，发现与用户机器相关的各种标识符被传输到微信的服务器。

## Methods 方法

In this section we explain our methods for analyzing WeChat’s data flows and tracking. Our primary analysis method is the use of reverse engineering. In our report, we analyzed the Android version of the app, specifically version 8.0.23 (android:versionCode = 2160) released on May 26, 2022, downloaded from the WeChat website. We used an account registered to a U.S. number for the analysis, which changes the behavior of the application compared to a mainland Chinese number. Our setup may not be comprehensive, and the full limitations are discussed in a section below.  

在本节中，我们将解释分析微信数据流和跟踪的方法。我们的主要分析方法是使用逆向工程。在我们的报告中，我们分析了该应用程序的 Android 版本，特别是 2022 年 5 月 26 日发布的 8.0.23 （android：versionCode = 2160） 版本，从微信网站下载。我们使用注册到美国号码的帐户进行分析，与中国大陆号码相比，这改变了应用程序的行为。我们的设置可能并不全面，下面的部分将讨论完整的限制。

### Reverse engineering methods  

逆向工程方法

In this work, we utilized both static and dynamic analysis methods, static referring to those methods which do not involve running an analyzed application and dynamic referring to those which do. For static analysis, we used [Jadx](https://github.com/skylot/jadx), a popular Android decompiler, to decompile WeChat’s Android Dex files into Java source code. We also used [Ghidra](https://ghidra-sre.org/) and [IDA Pro](https://hex-rays.com/ida-pro/) to analyze the native libraries bundled with WeChat.  

在这项工作中，我们同时使用了静态和动态分析方法，静态是指那些不涉及运行分析应用程序的方法，而动态是指那些涉及运行分析应用程序的方法。对于静态分析，我们使用流行的 Android 反编译器 Jadx 将微信的 Android Dex 文件反编译为 Java 源代码。我们还使用 Ghidra 和 IDA Pro 来分析与微信捆绑的原生库。

For dynamic analysis, we analyzed the application installed on a rooted Google Pixel 4 phone and an emulated Android OS, using [Frida](https://frida.re/) to hook into the app’s functions and manipulate and export application memory. We also performed network analysis of WeChat’s network traffic using [Wireshark](https://www.wireshark.org/). However, due to WeChat’s use of nonstandard cryptographic libraries like MMTLS, standard network traffic analysis tools that might work with HTTPS/TLS do not work for all of WeChat’s network activity. Our use of Frida was paramount for capturing the data and information flows we detail in this report. These Frida scripts are designed to intercept WeChat’s request data immediately before WeChat sends it to its MMTLS encryption module. The Frida scripts we used are published in [our Github repository](https://github.com/citizenlab/wechat-report-data).  

为了进行动态分析，我们分析了安装在有根的 Google Pixel 4 手机和模拟的 Android 操作系统上的应用程序，使用 Frida 挂接到应用程序的功能并操作和导出应用程序内存。我们还使用 Wireshark 对微信的网络流量进行了网络分析。但是，由于微信使用MMTLS等非标准加密库，因此可能与HTTPS/TLS一起使用的标准网络流量分析工具并不适用于微信的所有网络活动。我们对 Frida 的使用对于捕获我们在本报告中详细介绍的数据和信息流至关重要。这些Frida脚本旨在在微信将微信的请求数据发送到其MMTLS加密模块之前立即拦截微信的请求数据。我们使用的 Frida 脚本发布在我们的 Github 存储库中。

Using these dynamic analysis methods, we then manually simulate multiple common “user activities” that a user may perform in practice. The discrete user activities we tested are as follows:  

使用这些动态分析方法，我们手动模拟用户在实践中可能执行的多个常见“用户活动”。我们测试的离散用户活动如下：

-   Account creation 帐户创建
-   Account login 账户登录
-   Loading messages 加载消息
-   Sending messages 发送消息
-   Sending multimedia messages, including images and video  
    
    发送彩信，包括图像和视频
-   Loading Moments feed 加载时刻提要
-   Posting Moments 发布朋友圈
-   Posting multimedia Moments, including images and video  
    
    发布多媒体朋友圈，包括图片和视频
-   Commenting and interacting with Moments  
    
    评论和互动朋友圈
-   Mini Program usage 小程序使用

For each of these activities we identify the destination of all network requests made during them and record the types of data transmitted during them. We collect data under two primary modes: a “permissive” and “restrictive” mode. In a “permissive” mode, we grant the application all sensitive permissions, to demonstrate to what extent permissioned APIs are relied on during regular operation of the app.  

对于这些活动中的每一个，我们都会确定在它们之间发出的所有网络请求的目的地，并记录它们之间传输的数据类型。我们以两种主要模式收集数据：“允许”和“限制”模式。在“宽松”模式下，我们向应用程序授予所有敏感权限，以演示在应用程序的常规操作期间在多大程度上依赖于许可的 API。

To detect sensitive content flows, we identify various pieces of sensitive data related to the current user. For certain fields that are user-controllable, we use identifiable strings of text. We then attempt to find these pieces of data in WeChat’s plaintext, uncompressed transmissions. For instance, we identified the following information to track their transmissions:  

为了检测敏感内容流，我们会识别与当前用户相关的各种敏感数据。对于某些用户可控制的字段，我们使用可识别的文本字符串。然后，我们尝试在微信的明文、未压缩的传输中找到这些数据。例如，我们确定了以下信息来跟踪他们的传输：

-   Network carrier 网络运营商
-   Phone number 电话号码
-   User’s internal WeChat ID  
    
    用户内部微信号
-   OS details – Android API version  
    
    操作系统详细信息 – Android API 版本
-   Device details – model, brand  
    
    设备详细信息 – 型号、品牌

For spoofable numeric data, such as geolocation coordinates or screen size on an Android emulator, we search for the combination of certain numbers (such as both the width and height, or all three geocoordinates) to avoid matching false positives. For fully user-controllable fields, we inject recognizable and descriptive names, such as “USERNAME\_XXXXX” for the name of the account. A full list of identified information used to track content flows can be found in our [Github repository](https://github.com/citizenlab/wechat-report-data).  

对于可欺骗的数字数据（例如地理位置坐标或 Android 模拟器上的屏幕大小），我们会搜索某些数字的组合（例如宽度和高度，或所有三个地理坐标），以避免匹配误报。对于完全由用户控制的字段，我们注入可识别的描述性名称，例如帐户名称的“USERNAME\_XXXXX”。可以在我们的 Github 存储库中找到用于跟踪内容流的已识别信息的完整列表。

#### Mini Programs 小程序

In order to study WeChat behavior during Mini Program usage, we load “[WeChat Example Mini Program](https://github.com/wechat-miniprogram),” which is a test application that can trigger various API calls. We also collect data from five popular Mini Programs across different categories from 2021 from [a few](http://www.mpgcw.com/5872.html) [blog posts](https://zhuanlan.zhihu.com/p/459966259), based on usage and search metrics, since there is no Mini Program ordering provided by WeChat. The five Mini Programs we studied were Meituan (food), Pinduoduo (online shopping), Didi Chuxing (taxi service), Tongcheng Travel (tourism), and Kuaishou (online video). In these five Mini Programs, we simply browsed their main interface without logging in to them.  

为了研究微信在小程序使用过程中的行为，我们加载了“微信示例小程序”，这是一个可以触发各种 API 调用的测试应用程序。我们还从几篇博文中收集了 2021 年不同类别的五个热门小程序的数据，基于使用情况和搜索指标，因为微信没有提供小程序排序。我们研究的五个小程序分别是美团（美食）、拼多多（网购）、滴滴出行（出租车服务）、同程旅行（旅游）和快手（在线视频）。在这五个小程序中，我们只是浏览了它们的主界面，而没有登录它们。

### Limitations 局限性

This investigation only looks at client behavior, and is subject to other common limitations in privacy research that can only perform client analysis. Much of the data that is sent to WeChat servers may be required for functionality of the application. For instance, WeChat servers can certainly see chat messages since WeChat can censor them according to their content. We cannot say what WeChat is doing with the data that they collect, but we can make inferences about what is possible. Certain limited inferences about data sharing can be made based on prior work like this [report](https://citizenlab.ca/2020/05/we-chat-they-watch/), which indicates that messages sent by non-mainland-Chinese users are used to train censorship algorithms for mainland Chinese users. In this report, we focus on the version of WeChat for non-mainland-Chinese users.  

此调查仅着眼于客户行为，并受到隐私研究中其他常见限制的约束，这些限制只能执行客户分析。发送到微信服务器的大部分数据可能是应用程序功能所必需的。例如，微信服务器当然可以看到聊天消息，因为微信可以根据其内容对其进行审查。我们不能说微信正在用他们收集的数据做什么，但我们可以推断出什么是可能的。关于数据共享的某些有限推论可以基于先前的工作，如这份报告，这表明非中国大陆用户发送的消息被用来训练中国大陆用户的审查算法。在这份报告中，我们重点介绍了面向非中国大陆用户的微信版本。

Our investigation was also limited due to legal and ethical constraints. It has become increasingly difficult to obtain Chinese phone numbers for investigation due to the strict phone number and associated government ID requirements. Therefore, we did not test on Chinese phone numbers, which causes WeChat to behave differently. In addition, without a mainland Chinese account, the types of interaction with certain features and Mini Programs were limited. For instance, we did not perform financial transactions on the application.  

由于法律和道德限制，我们的调查也受到限制。由于严格的电话号码和相关的政府身份证要求，获取中国电话号码进行调查变得越来越困难。因此，我们没有对中国电话号码进行测试，这导致微信的行为有所不同。此外，如果没有中国大陆账号，与某些功能和小程序的交互类型受到限制。例如，我们没有在应用程序上执行金融交易。

In terms of our environment, we only investigated the Android application on a rooted Google Pixel 4 and an emulator for that same device, both on Android 12. Though we did not observe any operational differences in behavior between using the emulator and a regular device, there may be downstream effects to our use of an emulator to collect much of the data in this report.  

就我们的环境而言，我们只调查了 Android 12 上扎根的 Google Pixel 4 上的 Android 应用程序和同一设备的模拟器。尽管我们没有观察到使用模拟器和常规设备之间的任何操作差异，但我们使用模拟器来收集本报告中的大部分数据可能会产生下游影响。

We also only evaluated a recent version of WeChat (8.0.23 released on May 26, 2022). Testing different versions of WeChat, the backwards-compatibility of the servers with older versions of the application, and testing on a variety of Android operating systems with variations in API version, are great avenues for future work.  

我们也只评估了微信的最新版本（2022 年 5 月 26 日发布的 8.0.23）。测试不同版本的微信，服务器与旧版本应用程序的向后兼容性，以及在各种具有API版本变化的Android操作系统上进行测试，是未来工作的绝佳途径。

We also acknowledge that the scope of the Mini Programs work is limited compared to the size of the entire ecosystem, as we only take a few Mini Programs to investigate thoroughly. We attempt to offset this by focusing on the relationship between Mini Program API calls and data sent back to WeChat servers. A comprehensive and representative overview of the entire ecosystem would be a great avenue for future work.  

我们也承认，与整个生态系统的规模相比，小程序的工作范围是有限的，因为我们只需要几个小程序来彻底调查。我们试图通过关注小程序 API 调用和发送回微信服务器的数据之间的关系来抵消这一点。对整个生态系统进行全面和有代表性的概述将是未来工作的重要途径。

Finally, the WeChat codebase is vast. Over the years, the application has grown to cover various features, including ones that may transmit especially sensitive data (such as linking financial data and performing financial transactions). In this work, we do not purport to cover all of them. In fact, our research packages our preliminary understanding of WeChat. We provide our most accurate understanding of the codebase, but acknowledge that there exist limitations in our methodology and the vast nature of the WeChat application.  

最后，微信代码库非常庞大。多年来，该应用程序已经发展到涵盖各种功能，包括可能传输特别敏感数据的功能（例如链接财务数据和执行金融交易）。在这项工作中，我们并不打算涵盖所有这些。事实上，我们的研究包含了我们对微信的初步理解。我们提供了对代码库最准确的理解，但承认我们的方法论和微信应用程序的广泛性质存在局限性。

## Findings 发现

In this section we detail our findings concerning WeChat’s tracking during regular application usage as well as during mini-program usage. Further technical detail, such as the structure of network data and how we captured this data, can be found in the [Appendix](https://citizenlab.ca/2023/06/privacy-in-the-wechat-ecosystem-full-report/#appendix "Appendix") and in [our Github repository](https://github.com/citizenlab/wechat-report-data).  

在本节中，我们将详细介绍微信在常规应用程序使用期间以及小程序使用期间的跟踪发现。进一步的技术细节，例如网络数据的结构以及我们如何捕获这些数据，可以在附录和我们的 Github 存储库中找到。

### First-party tracking on Mini Programs  

小程序第一方追踪

The data collection observed on Mini Programs is likely in-place to enable the application monitoring and analytics features provided by WeChat, namely, “[We分析](https://wedata.weixin.qq.com/mp2/login)” or “WeAnalyze”. According to the “[WeAnalyze Mini Programs data analytics platform integration guide](https://developers.weixin.qq.com/community/business/doc/000082904b00c088bc8c5a2fa5c80d)”, there are two data dashboards that can be enabled by the Mini Program developer:  

在小程序上观察到的数据收集很可能是为了启用微信提供的应用程序监控和分析功能，即“We分析”或“WeAnalyze”。根据《WeAnalyze小程序数据分析平台集成指南》中，小程序开发者可以开启两个数据仪表盘：

-   Basic dashboard: No manual data upload needed. Contains visitor traffic data.  
    
    基本仪表板：无需手动上传数据。包含访客流量数据。
-   Advanced dashboard: Need to upload data using the wx.reportEvent API in the Mini Program. The dashboard shows the uploaded data.  
    
    高级仪表盘：需要使用小程序中的 wx.reportEvent API 上传数据。仪表板显示上传的数据。

All Mini Programs we studied collect at least basic user traffic data, and there is no notice to users. To put this data collection into perspective, it would be an equivalent privacy violation if Google Play Store automatically injected Google Analytics tracking scripts into all applications that were available on the platform.  

我们研究的所有小程序都至少收集了基本的用户流量数据，并且没有通知用户。从这个数据收集的角度来看，如果 Google Play 商店自动将 Google Analytics 跟踪脚本注入平台上可用的所有应用程序中，那将是等效的隐私侵犯。

During regular Mini Program usage, user interactions are sent back to WeChat servers. In addition, extremely verbose logging data is sent to WeChat servers during Mini Program usage; we do not observe this type of logging data sent during any of our other experiments. Many of the requests observed, especially extraneous logging and activity tracking, do not serve a baseline functionality for the Mini Programs, instead records and tracks user behavior across the program.  

在正常使用小程序期间，用户交互会被发送回微信服务器。此外，在小程序使用过程中，极其冗长的日志数据会发送到微信服务器;我们没有观察到在任何其他实验中发送的这种类型的记录数据。观察到的许多请求，尤其是无关的日志记录和活动跟踪，并不为小程序提供基线功能，而是记录和跟踪整个程序中的用户行为。

[![Illustration of a user interaction during Mini Program usage.](src=httpscitizenlab.cawp-contentuploads202306 "Should We Chat? Privacy in the WeChat Ecosystem 1")](https://citizenlab.ca/wp-content/webpc-passthru.php?src=https://citizenlab.ca/wp-content/uploads/2023/06/MMTLS-mini-program-network-request3.png&nocache=1)

Figure 1: Illustration of a user interaction during Mini Program usage.

### Details of tracking during Mini Program usage

The Java class JsApiOperateRealtimeReport (which pings endpoint /wxartrappsvr/route), sends the following data back to WeChat servers:

`    {    "appid": "wxe5f52902cf4de896",    "app_state": 1,    "appversion": "1.8.12",    "enter_scene": 1001,    "scene_note": "0",    "prescene": 0,    "sessionid": "hash=1505495844&ts=1681410111872&host=&version=671094583&device=2",    "add_state": 2,    "page_path": "page/animation/index",    "page_query": "{}",    "referpagepath": "",    "isentrance": 1,    "event_time": 1681410120047,    "sdk_version": "2.24.7",    "devicemodel": "sdk_gphone64_arm64",    "devicebrand": "google",    "os_name": "android",    "os_version": "Android 12",    "language_version": "en",    "networktype": "wifi",    "event_name": "expt_event_3",    "event_value": "{\"expt_data\":9}",    "unique_id": "1681410120047.2388",    "screen_width": 412,    "screen_height": 732,    "open_source": 1    }`

AppBrandIDKeyBatchReport (/wxausrevent/wxaappidkeybatchreport) sends a large stream of logging data, including API calls made by the Mini Program and other internal API calls made by the host platform, to WeChat servers.  

AppBrandIDKeyBatchReport（/wxausrevent/wxaappidkeybatchreport）向微信服务器发送大量日志数据，包括小程序的 API 调用和主机平台的其他内部 API 调用。

Finally, the class JsApiOperateWXData is also responsible for sending data back to WeChat servers, typically containing a Javascript API name and a custom serialized JSON blob of data. The JSON data sent in this object is primarily scoped to the functionality of the Javascript API at hand. Some of these network requests to WeChat servers may be necessary for the type of operation with the application; for instance, if the third-party application requests data about the logged-in WeChat user.  

最后，JsApiOperateWXData 类还负责将数据发送回微信服务器，通常包含 Javascript API 名称和自定义序列化 JSON blob 数据。在此对象中发送的 JSON 数据主要限定为手头的 Javascript API 的功能。其中一些对微信服务器的网络请求对于应用程序的操作类型可能是必需的;例如，如果第三方应用程序请求有关登录微信用户的数据。

More examples of each type of request can be found in our [Github repository](https://github.com/citizenlab/wechat-report-data).  

每种类型的请求的更多示例可以在我们的 Github 存储库中找到。

### Infrastructure and server locations  

基础结构和服务器位置

On testing from our vantage point in Canada, when logged out, the application primarily makes MMTLS requests to the domain **hkextshort.weixin.qq.com**. Once logged in, the application switches to using **sgshort.wechat.com** for MMTLS requests. Presumably, the prefixes “hk” and “sg” intend to refer to servers located in Hong Kong and Singapore, as outlined in WeChat’s [Privacy Policy](https://www.wechat.com/en/privacy_policy.html#pp_location). As expected, these hostnames resolved to IP addresses owned by Tencent, WeChat’s parent company.  

从我们在加拿大的有利位置进行测试时，当注销时，应用程序主要向域 hkextshort.weixin.qq.com 发出 MMTLS 请求。登录后，应用程序将切换到使用 sgshort.wechat.com 处理 MMTLS 请求。据推测，前缀“hk”和“sg”指的是位于香港和新加坡的服务器，如微信的隐私政策所述。正如预期的那样，这些主机名解析为微信母公司腾讯拥有的 IP 地址。

Upon startup, the application sends a regular HTTP GET request to the endpoint, [_http://dns.weixin.qq.com/cgi-bin/micromsg-bin/newgetdns_](http://dns.weixin.qq.com/cgi-bin/micromsg-bin/newgetdns), which is a formatted list of WeChat server domain names and associated IP addresses. This is combined with other MMTLS requests (for instance, we also observe MMTLS requests to _/cgi-bin/micromsg-bin/getcdndns_) to resolve certain IP addresses that the client might choose from. The full contents of this endpoint as we observed it can be found in our [Github repository](https://github.com/citizenlab/wechat-report-data).

In this file, we can identify a number of other prefixes, including “ml”, “sh”, “sz”, in addition to the “hk” and “sg” prefixes we observed. “sz” may stand for Shenzhen, the location of Tencent’s headquarters. Though it was not observed in our testing, requests to “szshort.weixin.qq.com” are commonly observed in [online](https://blog.naaln.com/2016/03/wechat-protocol-analysis/) [posts](https://github.com/Tornaco/Thanox/issues/403), possibly from developers located in China. This domain is also mentioned in a test case in some of [Tencent’s open-source networking code](https://github.com/Tencent/mars/blob/master/mars/stn/test_cases/hostorder_test.cc).

In general, we did not observe changes in the region prefix that was preferred by MMTLS requests. However, cross-referencing from existing data and observations by other researchers, we can conclude that the servers that are preferred by the WeChat application depend on a combination of IP address location, especially if the user is logged out, and the registered phone number locale (if the user is logged in).

### Opportunistic permissions

WeChat makes use of some dangerous permissions (as [defined](https://developer.android.com/guide/topics/permissions/overview#runtime) by Google), in particular “Location” and “Files and media”, during regular operation of the application, if those permissions are granted to the application.

In addition, a network request on opening the app contains an encrypted header containing [device serial numbers](https://citizenlab.ca/2015/05/the-many-identifiers-in-our-pocket-a-primer-on-mobile-privacy-and-security/), specifically the IMEI

and IMSI. On Android 10 devices and above, where the API no longer permits obtaining the IMEI, a dummy string “1234567890ABCDEF” is sent in place of the IMEI. Operating systems that do not have this protection in place would likely send the full IMEI.

These data points demonstrate that WeChat makes opportunistic use of device access to many types of sensitive data, which means hardening the operating system and device access to certain permissions does restrict the amount and type of data that is available to WeChat. However, in practice, this landscape is complicated by the fact that WeChat also manages the [permissions](https://developers.weixin.qq.com/miniprogram/en/dev/framework/open-ability/authorize.html) for its Mini Programs.

Any particular Mini Program can request an OS-level sensitive permission, such as reading storage or accessing the user location. In order to grant any Mini Program a particular permission, then, by design, WeChat must also request that permission from the operating system. There is no way to enable a particular permission for a Mini Program but not for the host WeChat application.

WeChat’s Mini Program ecosystem is often compared to an application ecosystem for a particular operating system; in this analogy, WeChat, or other super-apps, are akin to an operating system. OS-level permissioning systems have been studied at length in the past, and there are [an increasing](https://www.usenix.org/system/files/sec22-zhang-lei.pdf) [number of studies](https://arxiv.org/pdf/2205.15202.pdf) on the misuse of permission boundaries within super-apps.  

微信的小程序生态系统经常被比作特定操作系统的应用生态系统;在这个类比中，微信或其他超级应用程序类似于操作系统。操作系统级别的权限系统过去已经进行了深入研究，并且对超级应用程序内部滥用权限边界的研究越来越多。

### Tracking during regular application usage  

在常规应用程序使用期间进行跟踪

Here, we describe notable personal data tracking during general/regular application usage, outside the scope of what may be necessary for the operation of the WeChat application.  

在这里，我们描述了在一般/常规应用程序使用期间值得注意的个人数据跟踪，超出了微信应用程序运行所需的范围。

First, many WeChat MMTLS requests include, as a header:  

首先，许多微信 MMTLS 请求包括：

-   Platform data, specifically OS API version  
    
    平台数据，特别是 OS API 版本
-   User’s internal WeChat UID  
    
    用户内部微信UID

| **Data description 数据说明** | **Example 例** |
| --- | --- |
| Operating system details  
操作系统详细信息 | sdk\_gphone64\_arm64arm64-v8a |
| WeChat internal UIN 微信内部UIN | a 10-digit number 一个 10 位数字 |
| WeChat internal UID (“MMGUID”)  

微信内部 UID（“MMGUID”） | a 15 character hex string”A9543d226cb39f0f\_1683146442889″  

一个 15 个字符的十六进制字符串“A9543d226cb39f0f\_1683146442889” |
| API version API 版本 | android-32 安卓-32 |

_Table 1: Data items transmitted in WeChat MMTLS request headers.  

表 1：微信 MMTLS 请求头中传输的数据项。_

When the user opens the WeChat application, or logs into the WeChat application, a comprehensive device report is sent, including:  

当用户打开微信应用，或登录微信应用时，会发送一份全面的设备报告，包括：

| **Data description 数据说明** | **Example 例** |
| --- | --- |
| Phone number 电话号码 | Our U.S. testing phone number  
我们的美国测试电话号码 |
| IMEI IMEI的 | 1234567890ABCDEF (for Android 10+)  

1234567890ABCDEF （适用于 Android 10+） |
| Operating system details  

操作系统详细信息 | sdk\_gphone64\_arm64arm64-v8a |
| Manufacturer 制造者 | Google 谷歌 |
| Major OS release version  

主要操作系统版本版本 | 12 (Android 12) 12 （安卓 12） |
| Minor OS release version | 8015633 |
| [Build display name](https://developer.android.com/reference/android/os/Build#DISPLAY) | sdk\_gphone64\_arm64 12 S2B2.211203.006 8015633 |
| Network carrier | T-Mobile |

_Table 2: Data items transmitted when a user opens or logs into WeChat._

WeChat sends various batch reports that send application usage and monitoring data, as well as location data, if particular permissions are enabled by the user. A class called “CliReportKV” that collects and sends detailed logging messages that are collected over a large period of time, and “NetTypeReporter” sends networking and location data at a regular interval back to WeChat servers.

Finally, we find that when running with all permissions enabled, WeChat accesses the location API on any regular startup of the application, while logged in. Enabling location permissions automatically enables the “People Nearby” feature, which broadcasts your location so you can identify and interact with WeChat users nearby.

## Discussion

### Privacy policies and Weixin as “third party”

WeChat has a different privacy policy for its users, depending on whether the account is attached to a mainland Chinese mobile number. The [WeChat privacy policy](https://www.wechat.com/en/privacy_policy.html) refers to accounts with mainland Chinese mobile numbers as “Weixin accounts,” which are covered under a [separate privacy policy](https://weixin.qq.com/cgi-bin/readtemplate?lang=en_US&t=weixin_agreement&s=privacy&cc=CN&head=true). “Weixin” is a direct transliteration of WeChat’s Chinese name. We refer to these, respectively, as the WeChat privacy policy and the Weixin privacy policy.

Within the WeChat privacy policy, Weixin is referred to as a third party. The WeChat privacy policy also defers to the [Weixin privacy policy](https://weixin.qq.com/cgi-bin/readtemplate?lang=en_US&t=weixin_agreement&s=privacy&cc=CN&head=true) when it comes to first-party data collection on various features it designates as “[operated by Weixin](https://www.wechat.com/tpl/oversea/new/page/weixin_features/index?lang=en)”. In general, we note that various key features and services, such as Advanced Search and Channels, that tend to collect more user data, are all considered “third party services operated by Weixin” according to WeChat’s privacy policy. This separation between WeChat and Weixin features is not communicated within the application itself. Network data for both “WeChat services” and “Weixin services” all go to the same server, which seems to be determined by the user’s IP address or phone number, unlike other popular apps like [TikTok and its Chinese counterpart, Douyin](https://citizenlab.ca/2021/03/tiktok-vs-douyin-security-privacy-analysis/).

We identify additional privacy disclosure issues under this WeChat and Weixin dichotomy, and inconsistencies between the wording of these privacy policies to the observed behavior of the app.  

我们发现微信和微信二分法下的其他隐私披露问题，以及这些隐私政策的措辞与观察到的应用程序行为之间的不一致。

First, the WeChat privacy policy states that it will only share data with Weixin as necessary. However, app usage tracking for analytics is not necessary for the operation of the platform. In addition, we note that [prior research](https://citizenlab.ca/2020/05/we-chat-they-watch/) found that non-mainland-Chinese user data was being used to train censorship algorithms for mainland-Chinese users.  

首先，微信隐私政策声明，它只会在必要时与微信共享数据。但是，用于分析的应用程序使用情况跟踪对于平台的运行不是必需的。此外，我们注意到，先前的研究发现，非中国大陆用户数据被用于训练中国大陆用户的审查算法。

Second, the WeChat privacy policy implies that only third-party privacy practices and policies govern Mini Programs, when in fact, WeChat/Weixin also collect lots of data. In fact, Mini Programs are _not_ listed as subject to the [Weixin privacy policy](https://www.wechat.com/tpl/oversea/new/page/weixin_features/index?lang=en), and instead listed under “Weixin Open Platform,” which are only governed by third-party privacy policies.  

其次，微信隐私政策意味着只有第三方隐私惯例和政策才能管理小程序，而实际上，微信/微信也收集了大量数据。事实上，小程序并未被列为微信隐私政策的约束者，而是列在“微信开放平台”下，仅受第三方隐私政策的约束。

The Weixin privacy policy does mention that when using “Weixin’s Mini Programs,” they will collect data related to “logging in to, browsing, and using Mini Programs.” The wording of this translation is vague as to whether it refers to Mini Programs directly operated by Weixin, or all Mini Programs available on the Weixin platform.  

微信隐私政策确实提到，在使用“微信小程序”时，他们会收集与“登录、浏览、使用小程序”相关的数据。该译文的措辞含糊不清，究竟是指微信直接运营的小程序，还是微信平台上提供的所有小程序。

### Recommendations 建议

From our discussions above, we make the following recommendations to the platform and platform users to improve user privacy.  

通过上面的讨论，我们向平台和平台用户提出以下建议，以改善用户隐私。

#### Recommendations for WeChat:  

对微信的建议：

-   Remove forced enrollment of Mini Program analysis and tracking features, and change to an opt-in model. Currently, both developers and users are automatically enrolled into the We分析 tracking program with little notification. There is currently no way to opt-out of the program.  
    
    移除强制注册小程序分析和跟踪功能，改为选择加入模式。目前，开发人员和用户都会自动注册到 We分析 跟踪程序，几乎没有通知.目前无法选择退出该计划。

-   Enact a more fine-grained permissioning model. Certain Mini Programs might need permissions, but users should have some guarantee that the host platform cannot abuse those permissions if granted.  
    
    制定更精细的许可模型。某些小程序可能需要权限，但用户应该有一定的保证，即主机平台在被授予权限后不会滥用这些权限。
-   Remove the delineation between “Weixin” vs “WeChat” services in the Privacy Policy. Despite that the Privacy Policy claims certain core features of “WeChat” are run by a third-party named “Weixin,” there is no such delineation between “WeChat” and “Weixin” services in the regular operation of the application.  
    
    删除隐私政策中“微信”与“微信”服务之间的界限。尽管《隐私政策》声称“微信”的某些核心功能由名为“微信”的第三方运营，但在应用程序的正常运行中，“微信”和“微信”服务之间并无这样的界限。
-   Disclose WeChat’s first-party collection of Mini Program user data in the WeChat Privacy Policy.
-   Allow users to opt-out of analytics tracking during usage of “Weixin” services. Users should be able to opt-out of tracking that is not necessary to the function of the app.

#### Recommendations for users:

-   Avoid features delineated as “Weixin” services if possible. We note that many core “Weixin” services (such as Search, Channels) as delineated by the Privacy Policy perform more tracking than core “WeChat” services.
-   Use stricter permissions. In modern versions of Android, it is possible to restrict certain permissions (like location access) to when the application asks for it. Given the opportunistic use of enabled permissions by the application and the lack of a more fine-grained permissioning model between Mini Programs and the host WeChat platform, we recommend locking down application permissions.  
    
    使用更严格的权限。在现代版本的 Android 中，可以将某些权限（例如位置访问）限制在应用程序请求时。鉴于应用对使能权限的投机性使用，以及小程序与主机微信平台之间缺乏更细粒度的权限模型，我们建议锁定应用权限。
-   Update your device’s OS regularly for security features. Many new security features on modern versions of Android are working correctly to enforce permission boundaries and limit certain types of identifiers that are available to the application (such as IMEI). We recommend using an OS that has all of these features in place, and regularly updating for additional security features down the line.  
    
    定期更新设备的操作系统，了解安全功能。新版 Android 上的许多新安全功能都可以正常工作，以强制实施权限边界并限制应用可用的某些类型的标识符（例如 IMEI）。我们建议使用具有所有这些功能的操作系统，并定期更新以提供其他安全功能。

We note that these improvements are incremental at best, and recommendations for users should be taken in context with a particular threat model. For users with certain high risk profiles, no amount of these adjustments will make WeChat completely safe to use. While we would generally suggest using alternative messaging applications if possible, we understand that most users use WeChat out of necessity, and that using more secure messaging applications can itself be a risk factor depending on the particular situation.  

我们注意到，这些改进充其量是渐进式的，应结合特定威胁模型的上下文来考虑对用户的建议。对于具有某些高风险特征的用户，再多的调整也无法使微信完全安全使用。虽然我们通常建议尽可能使用其他消息传递应用程序，但我们知道大多数用户使用微信是出于必要，并且根据特定情况，使用更安全的消息传递应用程序本身可能是一个风险因素。

## Acknowledgments 确认

We would like to thank Jakub Dałek, Jonathan Mayer, Prateek Mittal, and Masashi Nishihata for their guidance and feedback on this project and report. Research for this project was supervised by Ron Deibert.  

我们要感谢 Jakub Dałek、Jonathan Mayer、Prateek Mittal 和 Masashi Nishihata 对这个项目和报告的指导和反馈。该项目的研究由Ron Deibert监督。

## Appendix: Program components related to network requests  

附录：与网络请求相关的程序组件

The contents of each MMTLS network message we captured included a serialized [Protobuf](https://github.com/protocolbuffers/protobuf) object and a request URI that is internal to WeChat operation. From the deserialized, unencrypted data contents, associated metadata, and static analysis of code paths around these requests, we can infer the purpose and usage of this particular data.  

我们捕获的每个 MMTLS 网络消息的内容都包括一个序列化的 Protobuf 对象和一个微信操作内部的请求 URI。从反序列化、未加密的数据内容、关联的元数据以及围绕这些请求的代码路径的静态分析中，我们可以推断出这些特定数据的用途和用途。

WeChat internally provides a unified Java API for components to make network requests. Each API endpoint is represented in a Java class (which we refer to as “API class”) that is extended from the NetSceneBase class.  

微信内部为组件提供统一的 Java API 进行网络请求。每个 API 端点都表示在一个 Java 类（我们称之为“API 类”）中，该类是从 NetSceneBase 类扩展而来的。

Each API class defines the following important properties:  

每个 API 类都定义以下重要属性：

-   Internal URI, usually starts with /cgi-bin/.  
    
    内部 URI，通常以 /cgi-bin/ 开头。
-   Request type, usually a 3 to 4 digit integer.  
    
    请求类型，通常为 3 到 4 位整数。

The most important API interfaces during request making are:  

发出请求期间最重要的 API 接口是：

-   NetSceneQueue.checkAndRun(): Starting a request of a specific API class. This function is a fixed implementation in NetSceneBase. This function is invoked from external components that need to make network requests.  
    
    NetSceneQueue.checkAndRun（）：启动特定 API 类的请求。此函数是 NetSceneBase 中的固定实现。此函数是从需要发出网络请求的外部组件调用的。
-   NetSceneBase.doScene() : Filling data fields. Implemented in API class.  
    
    NetSceneBase.doScene（） ：填充数据字段。在 API 类中实现。
-   GYNetEndI.onGYNetEnd() : Callback when response is received. Implemented in the API class.  
    
    GYNetEndI.onGYNetEnd（） ：收到响应时的回调。在 API 类中实现。

In the rest of this section, we illustrate the structure outlined above with a real API class: NetSceneEncryptCheckResUpdate. Note that most of the symbol names are given by us based on our understanding of its purpose.  

在本节的其余部分，我们将使用一个真实的 API 类来说明上面概述的结构：NetSceneEncryptCheckResUpdate。请注意，大多数符号名称都是我们根据对其用途的理解给出的。

[![Screenshot of the structure of a real API class.](src=httpscitizenlab.1.cawp-contentuploads202306 "Should We Chat? Privacy in the WeChat Ecosystem 2")](https://citizenlab.ca/wp-content/webpc-passthru.php?src=https://citizenlab.ca/wp-content/uploads/2023/06/image1.png&nocache=1)

_Figure 2: NetSceneEncryptCheckResUpdate.getType() decompiled.  

图 2：NetSceneEncryptCheckResUpdate.getType（） 已反编译。_

In NetSceneEncryptCheckResUpdate, the _request type_ is either 784 or 722 depending on the value of a configuration EcdhMgr.auth\_info\_prefs\_use\_new\_ecdh.  

在 NetSceneEncryptCheckResUpdate 中，请求类型为 784 或 722，具体取决于配置EcdhMgr.auth\_info\_prefs\_use\_new\_ecdh的值。

NetSceneEncryptCheckResUpdate’s request URI is defined in its subclass EncryptCheckResUpdateRR. The URI also depends on the configuration value EcdhMgr.auth\_info\_prefs\_use\_new\_ecdh.  

NetSceneEncryptCheckResUpdate 的请求 URI 在其子类 EncryptCheckResUpdateRR 中定义。URI 还取决于EcdhMgr.auth\_info\_prefs\_use\_new\_ecdh的配置值。

[![Screenshot of a request URI.](src=httpscitizenlab.2.cawp-contentuploads202306 "Should We Chat? Privacy in the WeChat Ecosystem 3")](https://citizenlab.ca/wp-content/webpc-passthru.php?src=https://citizenlab.ca/wp-content/uploads/2023/06/image2.png&nocache=1)

_Figure 3: EncryptCheckResUpdateRR.getUri() decompiled.  

图 3：EncryptCheckResUpdateRR.getUri（） 已反编译。_

NetSceneEncryptCheckResUpdate inherits most of its properties and methods from AbstractNetsceneCheckresUpdate, which implements doScene.  

NetSceneEncryptCheckResUpdate 从实现 doScene 的 AbstractNetsceneCheckresUpdate 继承其大部分属性和方法。

[![Screenshot of a decompiled class.](src=httpscitizenlab.3.cawp-contentuploads202306 "Should We Chat? Privacy in the WeChat Ecosystem 4")](https://citizenlab.ca/wp-content/webpc-passthru.php?src=https://citizenlab.ca/wp-content/uploads/2023/06/image3.png&nocache=1)

Figure 4: AbstractNetsceneCheckresUpdate.doScene() decompiled.  

图 4：AbstractNetsceneCheckresUpdate.doScene（） 已反编译。

AbstractNetsceneCheckresUpdate also implements onGYNetEnd.  

AbstractNetsceneCheckresUpdate 还实现了 onGYNetEnd。

[![Screenshot of a decompiled class.](src=httpscitizenlab.4.cawp-contentuploads202306 "Should We Chat? Privacy in the WeChat Ecosystem 5")](https://citizenlab.ca/wp-content/webpc-passthru.php?src=https://citizenlab.ca/wp-content/uploads/2023/06/image4.png&nocache=1)

Figure 5: AbstractNetsceneCheckresUpdate.onGYNetEnd() decompiled.  

图 5：AbstractNetsceneCheckresUpdate.onGYNetEnd（） 反编译。

Finally, when is this request sent? We see NetSceneQueue.checkAndRun() called with NetSceneEncryptCheckResUpdate only in a simple wrapper within the class itself:  

最后，此请求何时发送？我们看到 NetSceneQueue.checkAndRun（） 仅在类本身的简单包装器中使用 NetSceneEncryptCheckResUpdate 调用：

[![Screenshot of a decompiled class.](src=httpscitizenlab.5.cawp-contentuploads202306 "Should We Chat? Privacy in the WeChat Ecosystem 6")](https://citizenlab.ca/wp-content/webpc-passthru.php?src=https://citizenlab.ca/wp-content/uploads/2023/06/image5.png&nocache=1)

Figure 6: NetSceneEncryptCheckResUpdate.checkAndRun() decompiled.  

图 6：NetSceneEncryptCheckResUpdate.checkAndRun（） 已反编译。

The wrapper checkandrun() is called from com.tencent.mm.ui.LauncherUI.onCreate(), which is called during the application startup. This fits our traffic observation that API request /cgi-bin/micromsg-bin/secencryptcheckresupdate gets sent during application startup.  

包装器 checkandrun（） 是从 com.tencent.mm.ui.LauncherUI.onCreate（） 调用的，在应用程序启动时调用。这符合我们的流量观察，即在应用程序启动期间发送 API 请求 /cgi-bin/micromsg-bin/secencryptcheckresupdate。

More examples of request types, request data structures can be found in [our Github repository](https://github.com/citizenlab/wechat-report-data).  

更多请求类型、请求数据结构示例可以在我们的 Github 存储库中找到。
