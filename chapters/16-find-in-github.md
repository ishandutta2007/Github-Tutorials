# GitHub Treasure Hunting Guide

As a seasoned consultant and programmer, GitHub is the best tool I've ever used, because Google isn't always that helpful. GitHub is a treasure trove, but without a treasure map, its 100 million repositories have nothing to do with you. Over the years, I've mastered certain techniques, so writing an article to document them seems natural.

The summary is: GitHub is for searching things Google can't find. The reason they work is because **someone has already walked the path we want to take**. If you're taking a completely new path, this article might not mean much to you.

## Finding Demos to Save Time

Using new technology at work is quite different from personal practice. At work, we lean towards goal-oriented programming, with much higher demands on speed and time than during personal time. Once under this pressure, I turn to GitHub to find relevant demos, understand the principles, try them out a bit, and then introduce them into the project.

At this point, I search by **technology stack keywords and sort by update time** to see if there are suitable demos.

Life is short. If every time we try a new technology, we always have to write our own demo, writing multiple demos would take half a day or eight hours. Calculated this way, there's even less time left for other things. Trying official demos is often easier. But when writing applications, we always need to integrate with the current context. This integration isn't easy, with dependency conflicts, introducing third-party dependencies, etc.

**Friendly reminder**: **For simple projects, writing your own demo is much more convenient.** Trying out a project has a cost. If you need to try multiple projects, you might waste time.

## Finding Boilerplates: Accelerating Initial Development

Whether it's backend microservices architecture or frontend applications, application architecture is becoming complex. Backend microservices require combining various frameworks. Even a tool like `Spring Initializr` can only help us set up the project. We still need to work with other tools to build a basic system. It's similar for frontend applications. For large, comprehensive frameworks like Angular, the time spent isn't much. For smaller, elegant frameworks that require composition like React, using the official `create-react-app` can hardly produce what we want. Finding a suitable boilerplate is a better choice.

At this point, we can directly use the technology stack + keywords like `boilerplate` or `starter` to search, e.g., `react boilerplate`. If the combination found doesn't meet your requirements, then add the relevant technology stack keyword, like `react redux boilerplate`. Interestingly, Google might be more convenient than GitHub for this.

**Friendly reminder**: We need to consider: **Is the cost of modifying a boilerplate faster than starting from scratch?**

## Finding awesome-xxx: Exploring Possibilities

When practicing new frameworks, I'm used to **writing a series of related demo projects and then using awesome-xxx to explore possibilities.**

The Awesome-xxx series is the easiest type to earn Stars on GitHub. Almost any field, language, or framework with a certain knowledge base has its own awesome-xxx project, like awesome-python, awesome-iot, awesome-react, etc. In such projects, content is organized with a certain knowledge system, making indexing and searching convenient. If you want to enter a new field or try something new, search for `awesome xxx`.

**Friendly reminder**: awesome-xxx only means they include as many resources as possible, not that they have all related libraries.

## **Imitating Wheels** Wheels

In university, while practicing writing embedded operating systems, uC/OS-II was too complex for me as a beginner—too much irrelevant code. So I searched online for related implementations and found some, gradually improving the operating system based on those.

Learning a mature framework directly by reading existing source code is too costly and not economical. The best way is to build a wheel. Imitating a wheel first, then building your own, is the least labor-intensive way. Combined with the article "[Creating Wheels and Generating Wheels from GitHub](https://www.phodal.com/blog/create-framework-from-github/)", you can probably write a series of frameworks. Many people have the idea to build a similar wheel. Especially for a mature framework, there are often many imitations.

So, when you want to understand a framework and build a wheel, try searching for `xxx-like` or `xxx-like framework`. In Chinese, it's `仿 react 框架` (imitation react framework) or `类 react` (like react). For example, searching Google for `react-like` will find `inferno`. However, given GitHub's nature, finding such frameworks isn't easy. Google is often better than GitHub search for this.

So, it's suggested: **Search for related wheels during work breaks, then you can build wheels at home.**

## Learning Resources

GitHub has a vast amount of learning resources, from various articles and notes to all sorts of e-books. For example:

 1. Just search: `topic + 笔记` (topic + notes), e.g., `操作系统 笔记` (operating system notes) to find some OS-related notes.
 2. Just search: `book title` to find resources related to that book, e.g., `重构 改善既有代码的设计` (Refactoring: Improving the Design of Existing Code).

At the same time, GitHub also hosts various **unauthorized** translations of English books or PDFs of various e-books. As an author and translator of multiple books, I certainly don't encourage finding pirated books on GitHub.

And there are repositories on GitHub that provide learning resources, like [free-programming-books-zh_CN](https://github.com/justjavac/free-programming-books-zh_CN), an index of free Chinese programming books.

Suggestion: **Please respect copyright**, hahaha.

## Keys/Passwords

There's too much of this stuff on GitHub. Although I haven't been lucky enough to find a suitable key at the right time, many data leaks and database breaches are related to keys and passwords existing on GitHub.

However, fortunately, GitHub is already working on this issue: automatically deleting related commits, code warnings, etc.

## Private, Commercial SDKs or Code

Some people always submit some commercial code or internal company code to GitHub. If you occasionally see such code, besides informing the author promptly, you can also secretly clone the code—though it's not right, I still want to look.

For example, in ThoughtWorks' interview process, there's a coding assignment step, and personal implementations are not to be made public. When receiving an assignment, I always search GitHub to see if the corresponding code has been submitted. If it has, I need to remind the candidate.

In the past, when using Phaser to write applications, the corresponding particle system was paid. Since I was just trying it out, I didn't intend to buy it. I thought it might be on GitHub, so I searched for `particle-storm.js` and hit the jackpot. Then I happily wrote my Hello, World, only to find it too resource-intensive and gave up.

Suggestion: **Once you obtain someone else's commercial code on GitHub, please use it only for learning and always keep a low profile.** Carelessness could lead to legal trouble.

## Data and Data Generation Tools

When we need data, we consider writing crawlers. So GitHub is filled with all sorts of crawlers. Besides, some students even put the crawled data there. Once, when playing with ElasticSearch, I suddenly needed some real data for testing. I had to find a crawler and found some for dianping.com on GitHub.

The keyword was: `scrapy dianping.com`, obtained effortlessly.

Besides, with AI being so popular today, you can also find models trained by other students.

## Conclusion

Try your GitHub search function.