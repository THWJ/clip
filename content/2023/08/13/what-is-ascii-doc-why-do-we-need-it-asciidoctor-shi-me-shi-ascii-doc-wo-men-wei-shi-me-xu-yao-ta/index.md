---
title: What is AsciiDoc? Why do we need it?
date: 2023-08-13T07:23:37.000Z
updated: 2023-08-13T07:23:37.000Z
taxonomies:
  tags:
    - Tech
extra:
  source: https://asciidoctor.org/docs/what-is-asciidoc/
  hostname: asciidoctor.org
  author: Dan Allen
  original_title: What is AsciiDoc? Why do we need it? | Asciidoctor --- 什么是AsciiDoc？我们为什么需要它？
  original_lang: en

---

“_Writing is hard_.” “写作很难。”

That’s what experience has conditioned us to believe.  

这是经验使我们习惯于相信的。

But, we can’t just avoid it, especially in the tech industry. We _must_ write. Even the most brilliant software is useless without good documentation. If the users fail, so does the project.  

但是，我们不能只是避免它，特别是在科技行业。我们必须写信。没有好的文档，即使是最优秀的软件也是无用的。如果用户失败了，项目也会失败。

> Unless your UI discoverability is **really good**, saying “the feature isn’t documented” is the same as saying “the product can’t do it.”  
> 
> 除非你的UI的可发现性真的很好，否则说“这个功能没有文档记录”就等于说“这个产品做不到”。

— Nick Coghlan  \- 尼克·科格兰

In other words, 换句话说，

> Live and die by documentation.  
> 
> 文件决定生死。

— Matthew Ginnard  \- 马修·金纳德

Then why, _oh why_, do we make it more difficult by burying the content in XML schemas like DocBook, allowing complex word processors to distract us or wasting time battling with finicky WYSIWYG editors?  

那么，为什么，哦，为什么我们要把内容隐藏在DocBook之类的XML模式中，让复杂的字处理程序分散我们的注意力，或者浪费时间与挑剔的WYSIWYG编辑器作斗争，从而使事情变得更加困难呢？

Imagine if writing documentation was as simple as writing an email.  

想象一下，如果写文档就像写电子邮件一样简单。

_It **can** be_. 可以的

That’s the idea behind lightweight markup languages such as AsciiDoc. They offer a plain-text syntax, embellished with subtle, yet intuitive markup, that’s designed for humans to read, write and edit in raw form. The natural feel of the syntax keeps you focused on the content. Best of all, the plain text can quickly and easily be translated into output formats such as HTML5 for presentation.  

这就是AsciiDoc等轻量级标记语言背后的思想。它们提供了一种纯文本语法，用微妙而直观的标记进行修饰，这是为人类以原始形式阅读，编写和编辑而设计的。语法的自然感觉使您专注于内容。最重要的是，纯文本可以快速轻松地转换为HTML5等输出格式以进行演示。

In this introduction to AsciiDoc, we’ll cover what it is, why it’s valuable and what sets it apart from alternatives such as Markdown. You’ll discover that the key to escaping the agony of writing documentation is dropping the angle brackets that are burying the knowledge you have to share.  

在AsciiDoc的介绍中，我们将介绍它是什么，为什么它有价值，以及它与Markdown等替代品的区别。您会发现，摆脱编写文档的痛苦的关键是去掉尖括号，尖括号会埋没您必须分享的知识。

To learn how to reduce the work of writing and publishing content—whether it’s notes, documentation, articles, books, web pages or good ol’-fashioned prose—and attain writing zen, or to simply set the ideas locked in your head free, read on.  

要学习如何减少写作和发布内容的工作-无论是笔记，文档，文章，书籍，网页还是优秀的老式散文-并达到写作禅宗，或者只是将锁定在你脑海中的想法释放出来，请继续阅读。

## What is AsciiDoc? 什么是AsciiDoc？

AsciiDoc is two things:  

AsciiDoc是两件事：

1.  A mature<sup data-immersive-translate-effect="1" data-immersive_translate_walked="ec2c5671-2017-4d16-be45-b44f7c60872b">[<a id="_footnoteref_1" href="https://asciidoctor.org/docs/what-is-asciidoc/#_footnotedef_1" title="View footnote.">1</a>]</sup>, plain-text writing format for authoring notes, articles, documentation, books, ebooks, web pages, slide decks, blog posts, man pages and more.  
    
    一个成熟的 <sup data-immersive-translate-effect="1" data-immersive_translate_walked="ec2c5671-2017-4d16-be45-b44f7c60872b">[<a id="_footnoteref_1" href="https://asciidoctor.org/docs/what-is-asciidoc/#_footnotedef_1" title="View footnote.">1</a>]</sup> 纯文本写作格式，用于创作笔记、文章、文档、书籍、电子书、网页、幻灯片、博客文章、手册页等。
    
2.  A text processor and toolchain for translating AsciiDoc documents into various formats (called _backends_), including HTML, DocBook, PDF and ePub<sup data-immersive-translate-effect="1" data-immersive_translate_walked="ec2c5671-2017-4d16-be45-b44f7c60872b">[<a id="_footnoteref_2" href="https://asciidoctor.org/docs/what-is-asciidoc/#_footnotedef_2" title="View footnote.">2</a>]</sup>.  
    
    一个文本处理器和工具链，用于将AsciiDoc文档转换为各种格式（称为后端），包括HTML，DocBook，PDF和ePub <sup data-immersive-translate-effect="1" data-immersive_translate_walked="ec2c5671-2017-4d16-be45-b44f7c60872b">[<a id="_footnoteref_2" href="https://asciidoctor.org/docs/what-is-asciidoc/#_footnotedef_2" title="View footnote.">2</a>]</sup> 。
    

AsciiDoc belongs to the family of [lightweight markup languages](https://en.wikipedia.org/wiki/Lightweight_markup_language), the most renowned of which is [Markdown](https://daringfireball.net/projects/markdown/). AsciiDoc stands out from this group because it supports all the structural elements necessary for drafting articles, technical manuals, books, presentations and prose. In fact, it’s capable of meeting even the most advanced publishing requirements and technical semantics.  

AsciiDoc属于轻量级标记语言家族，其中最着名的是Markdown。AsciiDoc从这个群体中脱颖而出，因为它支持起草文章、技术手册、书籍、演示文稿和散文所必需的所有结构元素。事实上，它甚至能够满足最高级的发布需求和技术语义。

Serving as testament of this fact, many O’Reilly authors including [Matthew McCullough](https://github.com/matthewmccullough), [Tim Berglund](https://github.com/tlberglund), [Simon St.Laurent](https://github.com/oreillymedia/etudes-for-erlang), [Matt Neuburg](https://www.apeth.net/matt/iosbooktoolchain.html) and [Ian Darwin](https://www.oreilly.com/pub/au/219) have used AsciiDoc to write their books for that iconic technical library.  

作为这一事实的证明，包括Matthew McCullough，Tim Berglund，Simon St.Laurent，Matt Neuburg和Ian达尔文在内的许多O'Reilly作者都使用AsciiDoc为这个标志性的技术图书馆撰写书籍。

From the very beginning, AsciiDoc was designed to be a shorthand replacement for [DocBook](https://docbook.org/whatis), one of the formats AsciiDoc can generate. AsciiDoc can also produce beautiful HTML5, PDFs, eBooks, man pages and even slide decks. It has you covered from first draft to publishing.  

从一开始，AsciiDoc就被设计成DocBook的速记替代品，DocBook是AsciiDoc可以生成的格式之一。AsciiDoc还可以生成漂亮的HTML5，PDF，电子书，手册页甚至幻灯片。它涵盖了从第一稿到出版。

Now that we’ve established what AsciiDoc is, let’s consider why we need it.  

现在我们已经确定了AsciiDoc是什么，让我们考虑一下为什么需要它。

## Why AsciiDoc? 为什么选择AsciiDoc？

As humans, we have no difficulty talking or thinking. In fact, we’re fluent in it. It’s an activity that just happens whenever a thought comes to mind.  

作为人类，我们说话或思考都没有困难。实际上，我们都很熟练。这是一种只要有一个想法出现在脑海中就会发生的活动。

_Writing, on the other hand, rarely comes so easy.  

另一方面，写作很少如此容易。_

When it’s time to write our thoughts down, we _struggle_ to find the words—or, at least, how to arrange and organize them. That _damn_ inner critic disrupts the stream of consciousness we coast on while talking or thinking.  

当我们要把自己的想法写下来时，我们很难找到合适的词，或者至少是如何安排和组织它们。那个该死的内在批评者扰乱了我们说话或思考时的意识流。

It’s reasonable to conclude that writing is just hard.  

有理由得出结论说写作很难。

_Or is it? 是吗？_

### On writing: e-mail vs documents  

关于写作：电子邮件vs文档

Writing e-mail is easy. We do it all the time. Every day, we respond to dozens of e-mail and social media messages. That involves communication through writing. That’s right, _writing!_  

写电子邮件很容易。我们一直都这么做。每天，我们都会回复数十封电子邮件和社交媒体消息。这涉及到通过写作进行交流。没错，就是写作！

Yet, amid the flurry of typing that occurs when we respond to an e-mail, we hardly even realize we’re doing it…and _fluently!_  

然而，当我们回复电子邮件时，在打字的忙乱中，我们几乎没有意识到我们正在做这件事……而且很流利！

As it turns out…  

事实证明

> Most people are OK with writing e-mails. They don’t consider this writing. There’s no writer’s block. Someone asks you a question, you \[press\] reply and type away.  
> 
> 大多数人都可以写电子邮件。他们不认为这是写作。没有作家的瓶颈。有人问你一个问题，你（按下）回复，然后打字。

_So why do we struggle to write **documents**?  

那么，我们为什么要努力写文件呢？_

The main reason we struggle is because we don’t write documents the same way we write e-mail. Instead, we allow ourselves to get distracted by complex word processors, bury the content in XML schemas like DocBook, or battle with finicky WYSIWYG editors. How did we get ourselves into this mess?  

我们挣扎的主要原因是因为我们写文档的方式与写电子邮件的方式不同。相反，我们允许自己被复杂的字处理程序分散注意力，将内容隐藏在DocBook之类的XML模式中，或者与挑剔的WYSIWYG编辑器斗争。我们是怎么陷入这种困境的？

### Word processors, the real writer’s block  

文字处理机，真实的的写作瓶颈

When you’re in the writing (i.e., [typing](https://blog.stoyanstefanov.com/writing-vs-typing/)) phase, you want the words to flow onto the screen with minimal distractions and interruptions. Flow, not just time, is essential.  

当你在写作的时候（例如，打字）阶段，你希望单词在最小的干扰和中断下流到屏幕上。流动，而不仅仅是时间，是必不可少的。

Most word processors excel at distracting you from writing. The result: _you write less_ (ironic, huh?).  

大多数文字处理器擅长分散你写作的注意力。结果是：你写得更少了（讽刺的是吧？））.

In a word processor, before you can type the first word on a blank white screen, you’re forced to think about what font family you want, what font size you want, what lines spacing you want and so on. Once you do get going, auto-correct, spelling and grammar suggestions entice you to backtrack and lose your next thought. “Smart” quotes and auto-linking messes with the text as fast as you can enter it. If you paste text, it likely gets added to the document with a different font family, size and even color.  

在文字处理器中，在你可以在空白的白色屏幕上输入第一个单词之前，你不得不考虑你想要什么字体系列，你想要什么字体大小，你想要什么行距等等。一旦你开始，自动更正，拼写和语法建议诱使你回溯并失去你的下一个想法。“智能”引号和自动链接会以您输入的最快速度扰乱文本。如果您粘贴文本，它可能会以不同的字体系列，大小甚至颜色添加到文档中。

**Undo. Undo. Undo! 撤销。撤销。撤销**

Let’s not even talk about inserting source code. The designers of word processors clearly did not.  

让我们甚至不谈论插入源代码。文字处理器的设计者显然没有这样做。

**Format. Format. Format! 格式。格式。格式！**

After burning time fighting with its interface, you rightfully conclude that the word processor is trying to _sabotage_ your writing process.  

在与它的界面斗争了很长时间之后，你理所当然地得出结论，文字处理器正试图破坏你的写作过程。

**We _need_ an easier way to write!  

我们需要一个更简单的方式来写！**

But how? 但怎么做呢？

### Use what you know  

用你所知道的

_What if you could write documentation like you write e-mail?  

如果你能像写电子邮件一样写文档会怎么样？_

Imagine being able to forget about layout, typesetting, styling (and even some semantics) and just _write_. That’s the idea behind **lightweight markup languages** such as Markdown and AsciiDoc.  

想象一下，能够忘记布局、排版、样式（甚至一些语义），只写。这就是Markdown和AsciiDoc等轻量级标记语言背后的想法。

Here’s how John Gruber introduced Markdown (in March 2004):  

以下是John Gruber如何介绍Markdown（2004年3月）：

> The overriding design goal for Markdown’s formatting syntax is to make it as readable as possible.  
> 
> Markdown格式化语法的首要设计目标是使其尽可能易读。
> 
> A Markdown-formatted document should be publishable as-is, as plain text, without looking like it’s been marked up with tags or formatting instructions.  
> 
> Markdown格式的文档应该是可发布的，纯文本，而不像是标记或格式化说明。
> 
> The single biggest source of inspiration for Markdown’s syntax is the format of plain text e-mail.  
> 
> Markdown语法最大的灵感来源是纯文本电子邮件的格式。

— John Gruber, Creator of Markdown \- John Gruber，Markdown创始人

Similarly, here’s how Stuart Rackham introduced AsciiDoc (2 years earlier):  

类似地，以下是Stuart Rackham如何介绍AsciiDoc（2年前）：

> You write an AsciiDoc document the same way you would write a normal text document. There are no markup tags or weird format notations. AsciiDoc files are designed to be viewed, edited and printed directly or translated to other presentation formats.  
> 
> 编写AsciiDoc文档的方式与编写普通文本文档的方式相同。没有标记标签或奇怪的格式符号。AsciiDoc文件可直接查看、编辑和打印，或转换为其他演示格式。

— Stuart Rackham, Creator of AsciiDoc \- Stuart Rackham，AsciiDoc的创建者

These languages are designed to enable humans to write documents, and for other humans to be able to read them, **_as is_**, in _raw_ form.  

这些语言被设计成使人类能够编写文档，并且使其他人能够以原始形式阅读它们。

Here’s a basic example of an AsciiDoc document:  

下面是一个AsciiDoc文档的基本示例：

```
= Introduction to AsciiDoc
Doc Writer <doc@example.com>

A preface about https://asciidoc.org[AsciiDoc].

== First Section

* item 1
* item 2

[source,ruby]
puts "Hello, World!"
```

_It’s a plain text syntax…I **know** this!  

这是一个纯文本语法...我知道！_

Compare that to the same document written in DocBook:  

将其与DocBook中编写的相同文档进行比较：

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE article PUBLIC "-//OASIS//DTD DocBook XML V4.5//EN"
    "http://www.oasis-open.org/docbook/xml/4.5/docbookx.dtd">
<article lang="en">
  <articleinfo>
    <title>Introduction to AsciiDoc</title>
    <date>2013-01-01</date>
    <author>
      <firstname>Doc</firstname>
      <surname>Writer</surname>
      <email>doc@example.com</email>
    </author>
    <authorinitials>DW</authorinitials>
  </articleinfo>
  <simpara>
    A preface about
    <ulink url="http://asciidoc.org">AsciiDoc</ulink>.
  </simpara>
  <section id="_first_section">
    <title>First Section</title>
    <itemizedlist>
      <listitem>
        <simpara>item 1</simpara>
      </listitem>
      <listitem>
        <simpara>item 2</simpara>
      </listitem>
    </itemizedlist>
    <programlisting language="ruby"
        linenumbering="unnumbered">
      <![CDATA[puts "Hello, World!"]]>
    </programlisting>
  </section>
</article>
```

Yikes! 哎呀！

While DocBook (and HTML) may not be complex, they fail the readability test.  

虽然DocBook（和HTML）可能并不复杂，但它们无法通过可读性测试。

> DocBook is nice, but (like XML) it is not meant for editing nor for merging changes (by humans). Using AsciiDoc (which translates to DocBook perfectly) is a much easier way of developing.  
> 
> DocBook很好，但（像XML一样）它不适合编辑或合并更改（由人类）。使用AsciiDoc（它可以完美地转换为DocBook）是一种更容易的开发方式。

— Dag Wieers  \- 达格·威尔斯

AsciiDoc gets us back to what’s important: _writing_. You can drop those angle brackets, but you don’t have to drop the semantics. And it’s a syntax a human can actually edit, efficiently.  

AsciiDoc让我们回到重要的事情：写作您可以删除那些尖括号，但不必删除语义。这是一种人类可以有效编辑的语法。

> Use AsciiDoc for document markup. Really. It’s actually **readable** by humans, easier to parse and way more flexible than XML.  
> 
> 使用AsciiDoc进行文档标记。真的。它实际上是人类可读的，比XML更容易解析和灵活。

— Linus Torvalds  \- Linus Torvalds的

Here’s the really great thing about AsciiDoc. Worse case scenario, you convert it to DocBook as a common exchange format. DocBook is the “no lock-in” exit path for AsciiDoc. You decide AsciiDoc doesn’t work out, you can bail on it without losing a word. No need to invent another format. That’s why so many people are going all in on it.  

这是AsciiDoc真正伟大的事情。更糟糕的情况是，您将其转换为DocBook作为通用交换格式。DocBook是AsciiDoc的“无锁定”退出路径。你决定AsciiDoc不工作，你可以保释它没有失去一个字。不需要再创造新的格式。这就是为什么这么多人都在这上面。

## The zen of writing AsciiDoc  

编写AsciiDoc的禅

AsciiDoc is about being able to focus on expressing your ideas, writing with ease and passing on knowledge without the distraction of complex applications or angle brackets. In other words, it’s about discovering _writing zen_.  

AsciiDoc是关于能够专注于表达你的想法，轻松写作和传递知识，而不会被复杂的应用程序或尖括号分心。换句话说，这是关于发现写作禅。

AsciiDoc works because: AsciDoc的工作原理是：

-   It’s readable 这是可读的
    
-   It’s concise 很简洁
    
-   It’s comprehensive 很全面
    
-   It’s extensible 它是可扩展的
    
-   It produces beautiful output (HTML, DocBook, PDF, ePub and more)  
    
    它可以生成漂亮的输出（HTML、DocBook、PDF、ePub等）
    

AsciiDoc is easy to write and easy to read (in raw form). It’s also easy to proof and edit. After all, it’s plain text, just like that familiar e-mail.  

AsciiDoc很容易写，也很容易读（以原始形式）。它也很容易证明和编辑。毕竟，它是纯文本，就像熟悉的电子邮件一样。

The AsciiDoc syntax is intuitive because it recognizes time-tested, plain text conventions for marking up or structuring the text. The punctuation was carefully chosen to look like what it means. A user unfamiliar with AsciiDoc can figure out the structure and semantics (i.e., what you mean) just by looking at it. Best of all, **it only requires a text editor to read or write**.  

AsciiDoc语法是直观的，因为它识别用于标记或结构化文本的经过时间考验的纯文本约定。标点符号是经过精心挑选的，看起来像它的意思。不熟悉AsciiDoc的用户可以弄清楚结构和语义（即，你是什么意思）只是看着它。最好的是，它只需要一个文本编辑器来读取或写入。

AsciiDoc allows you to focus on the actual writing and only worry about tweaking the output when you are ready to convert the document. The plain-text of an AsciiDoc document is easily converted into a variety of output formats, beautifully formatted, without having to rewrite the content.  

AsciiDoc允许您专注于实际的写作，只需要在准备转换文档时调整输出即可。AsciiDoc文档的纯文本很容易转换成各种输出格式，格式精美，而无需重写内容。

Copy text from an e-mail into a document and see how quickly you can turn it into documentation. Almost immediately, you’ll find your writing zen and enjoy the rewarding experience of sharing knowledge.  

将电子邮件中的文本复制到文档中，看看将其转换为文档的速度有多快。几乎立即，你会发现你的写作禅和享受分享知识的有益经验。

Live or die by documentation?  

文件是生是死？  

“Live!”  “活！”

## Next steps 下一步

With an understanding of what AsciiDoc is and why it’s so desperately needed, you’re encouraged to delve into the AsciiDoc syntax covered in the [AsciiDoc Writer’s Guide](https://asciidoctor.org/docs/asciidoc-writers-guide). If you’re just looking for a cheat sheet, check out the [AsciiDoc Quick Reference](https://docs.asciidoctor.org/asciidoc/latest/syntax-quick-reference/). Hopefully you’ll agree the syntax just makes sense.  

了解了什么是AsciiDoc以及为什么如此迫切需要它，我们鼓励您深入研究AsciiDoc Writer's Guide中介绍的AsciiDoc语法。如果你只是在寻找一个备忘单，看看AsciiDoc快速参考。希望你会同意语法只是有意义的。
