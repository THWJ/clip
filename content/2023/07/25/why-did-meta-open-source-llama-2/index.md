---
title: ''
date: 2023-07-25T08:14:10.000Z
updated: 2023-07-25T08:14:10.000Z
taxonomies:
  tags:
    - Tech
extra:
  source: >-
    chrome-extension://mccnmpehoaaagnjojjdmiaaalpphhhhf/_generated_background_page.html
  hostname: mccnmpehoaaagnjojjdmiaaalpphhhhf
  author: Matt Rickard
  original_title: Why Did Meta Open-Source Llama 2?
  original_lang: en

---

## Why Did Meta Open-Source Llama 2?  

为什么元开源骆驼 2？

Llama 2 is a commercially-available open-source model from Meta that builds on LLaMA, the “academic-use only” model that was, in reality, generally available to anyone who could click a download link.  

Llama 2 是 Meta 的一个商业开源模型，它建立在 LLaMA 的基础上，LLaMA 是“仅限学术使用”的模型，实际上，任何可以点击下载链接的人都可以使用。

At a high level, many are familiar with strategic open-source from big technology companies — products like Android, Chrome, and Visual Studio Code. But why exactly would Meta make the weights of the Llama 2 commercially available? A more in-depth analysis.  

在高层次上，许多人熟悉大型科技公司的战略开源 - Android，Chrome和Visual Studio Code等产品。但是，为什么 Meta 会让 Llama 2 的重量商业化呢？更深入的分析。

The framework in _[A Short Taxonomy of Open-Source Strategies](https://matt-rickard.com/short-taxonomy-of-open-source-strategies)_ identifies 7 different categories of strategic power from open-source: **hiring, marketing, go-to-market (complement), go-to-market (free-tier), reduce competitor’s moat, goodwill,** and **standards lobbying.**  

开源战略简短分类法中的框架确定了开源的 7 种不同类别的战略力量：招聘、营销、上市（补充）、上市（免费层）、减少竞争对手的护城河、商誉和标准游说。

Likewise, a more specific framework applied to machine learning models in _[Why Open-Source a Model?](https://matt-rickard.com/why-open-source-a-model)_ lists four more specific reasons:   

同样，为什么要开源模型？列出了四个更具体的原因：

-   **You have proprietary data but not enough resources or expertise.  
    
    您拥有专有数据，但没有足够的资源或专业知识。**
    
-   **You want to recruit and retain top researchers.  
    
    您想招募和留住顶尖研究人员。**
    
-   **You sell hardware or cloud resources.  
    
    您销售硬件或云资源。**
    
-   **You have no distribution but have a breakthrough insight.  
    
    你没有分布，但有突破性的洞察力。**
    

Looking at the Llama 2 license hints at Meta’s goals.  

看看 Llama 2 许可证暗示了 Meta 的目标。

-   **No Improvements to Other Models**: _You will not use the Llama Materials or any output or results of the Llama Materials to improve any other large language model (excluding Llama 2 or derivative works thereof)._  
    
    不改进其他模型：您不得使用骆驼材料或骆驼材料的任何输出或结果来改进任何其他大型语言模型（不包括骆驼 2 或其衍生作品）。
    
-   **Restrictive Terms for Competitors**: _If, on the Llama 2 version release date, the monthly active users of the products or services made available by or for Licensee, or Licensee’s affiliates, is greater than 700 million monthly active users in the preceding calendar month, you must request a license from Meta, which Meta may grant to you in its sole discretion, and you are not authorized to exercise any of the rights under this Agreement unless or until Meta otherwise expressly grants you such rights._  
    
    竞争对手的限制性条款：如果在 Llama 2 版本发布日期，被许可方或被许可方的关联公司提供的或为被许可方提供的产品或服务的月活跃用户在上一个日历月的月活跃用户超过 7 亿，您必须向 Meta 申请许可，Meta 可以自行决定授予您许可， 并且您无权行使本协议项下的任何权利，除非或直到 Meta 另行明确授予您此类权利。
    
-   **No Trademark Licenses:** Retains branding and marketing rights.  
    
    无商标许可：保留品牌和营销权。
    

Using the framework, the launch announcement, and the license, some hypotheses on why Meta open-sourced Llama 2:  

使用框架、发布公告和许可证，关于 Meta 开源 Llama 2 的一些假设：

_**Reduce Competitor’s Moat.**_ Llama 2 hurts two kinds of competitors. The first is companies with proprietary models — Google and OpenAI (Microsoft, by association). The second is any company that sits in the serving stack but needs to organically build its audience (Meta has billions of captive users across its properties).   

减少竞争对手的护城河。骆驼2伤害了两种竞争对手。首先是拥有专有模型的公司——谷歌和OpenAI（Microsoft，通过关联）。第二种是任何位于服务堆栈中但需要有机地建立其受众的公司（Meta 在其属性中拥有数十亿专属用户）。

_**Go-to-market (free-tier or complement).**_ Llama 2 is available in 7b, 13b, and 70b parameter sizes. What if we viewed these smaller models as “freemium” self-serve? You build your infrastructure around the Llama 2 architecture and try it out on your own cloud, but use a future offering from Meta that is (1) extremely large or (2) hyper-up-to-date in an online way that most organizations couldn’t accomplish.   

进入市场（免费套餐或补充）。Llama 2 提供 7b、13b 和 70b 参数大小。如果我们将这些较小的模型视为“免费增值”自助服务会怎样？您围绕 Llama 2 架构构建基础架构，并在自己的云上试用，但使用 Meta 的未来产品，该产品 （1） 非常大或 （2） 以大多数组织无法完成的在线方式超最新。

What would be Meta’s complement that they are shipping? Possibilities:  

他们正在运送的 Meta 补充是什么？可能性：

-   LLM-enabled features for Instagram / Threads / Facebook.  
    
    适用于Instagram / Threads / Facebook的LLM功能。
    
-   Hardware — specially designed chips and data centers purpose-built for Llama.  
    
    硬件 — 专为 Llama 打造的芯片和数据中心。
    
-   ML Framework — Any Llama derivative will work best in PyTorch.  
    
    ML 框架 — 任何 Llama 衍生品在 PyTorch 中都运行得最好。
    
-   Future commercial offering — Managed Service  
    
    未来的商业产品 — 托管服务
    

_**Marketing**._ Meta could potentially develop a reputation as a company built on the cutting edge if they play their cards right. Google’s reputation did wonders for it for decades (until it didn’t) — developers, users, and the general media. Meta has a much bigger uphill battle here, but the general sentiment is shipping.  

营销。如果 Meta 打得好，他们可能会发展出一家建立在最前沿公司的声誉。几十年来，谷歌的声誉为它创造了奇迹（直到它没有）——开发者、用户和普通媒体。Meta 在这里有一场更大的艰苦战斗，但普遍的情绪是运输。

### Subscribe to Matt Rickard  

订阅马特·瑞卡德

Daily posts on engineering, startups, and AI.  

关于工程、初创公司和人工智能的每日帖子。

[![](https3A2F2Fsubstack-post-media.s3.amazonaws.com2Fpublic2Fimages2Fdf6bed7c-8df3-4dd9-98fa-73a38abd958c_1125x1122.jpeg)](https://substack.com/profile/5339722-alex-gorischek?utm_source=post-reactions-face)
