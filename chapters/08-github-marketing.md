How to Promote
===

Besides being good at writing md e-books to accumulate Stars, I have also written a series of open-source software and mastered some project operation skills.

**Open source isn't just about writing good software and a README; it also requires detailed documentation, example programs, and more**.

**Open source also doesn't mean that once your project is good, a bunch of people will automatically participate**.

**Open source also requires you to help others fix bugs, …**.

**People do things for a reason**, i.e., motivation. Let's give another example: if your project isn't popular enough and nobody has heard of it, then **putting it on your resume might not be very useful**.

Marketing First
---

Open source requires some marketing skills, which can help you attract attention. A simple example: Zhengmei Situ's [avalon](https://github.com/RubyLouvre/avalon) framework appeared early and did quite well in the MV* aspect, but its marketing was... lacking. As a result, many front-end developers in China aren't familiar with this framework. Otherwise, today in China, it might be the "AVRR" big four frameworks.

Vue didn't become popular just because it was easy to use. I have a particularly deep impression of this. At the time, I saw this project on GitHub Trending and found it couldn't work properly yet.

As mentioned in the article "[FIRST WEEK OF LAUNCHING VUE.JS](http://blog.evanyou.me/2014/02/11/first-week-of-launching-an-oss-project/)", the author made a series of marketing plans at the beginning of the project:

 - HackerNews
 - Reddit /r/javascript
 - EchoJS
 - The DailyJS blog
 - JavaScript Weekly
 - Maintain a project Twitter account

Additionally, the article also mentioned another article: "[How to Spread The Word About Your Code](https://hacks.mozilla.org/2013/05/how-to-spread-the-word-about-your-code/?utm_source=statuscode&utm_medium=email)".

This is quite interesting. If your idea is good, everyone will likely agree, click the link, and give you a Star. Then, you gain better motivation to do this. The project also gains considerable attention from the start. If people think your project lacks novelty, well, you know~.

Furthermore, another possibility is that your ID isn't fancy enough, meaning your influence in the community is limited. At this point, you need to **slowly accumulate popularity bit by bit**. Once you've accumulated some popularity, you can be like Yukihiro "Matz" Matsumoto, who had 1000+ Stars when he created mRuby. Moreover, there were related articles introduced in the community, and headlines were posted by his fans. For example, over a year ago, I created the [mole](https://github.com/phodal/mole) project.

![Mole](../img/mole.png)

At the time, it was to create a GitHub-based cloud note-taking tool for myself. When the project reached a certain level of completeness, I published a related introduction on my WeChat public account. The next day, it had 100+ Stars and received some encouraging words. Correspondingly, for the domestic market, there are:

 - GeekHeadlines
 - Juejin
 - DeveloperHeadlines
 - v2ex
 - Zhihu
 - My not-so-great Weibo

So, what do you think?

Writing a Good README
---

In an open-source project, the README is the most important content. It quickly introduces the project and determines whether it can attract users:

 - **What does this project do?**
 - **What problem does it solve?**
 - **What features does it have?**
 - **A hello, world example**

### What does this project do? – A One-Liner

GitHub's Description is the first introduction we see on Hacking News, GitHub Trending, etc. It's also what we can quickly tell others, as shown in the image below:

![GitHub Trending](../img/github-trending-example.png)

This one sentence must be simple and clear, explaining what it does.

For example, Angular's one-liner is: One framework. Mobile & desktop.

React's is: A declarative, efficient, and flexible JavaScript library for building user interfaces.

Vue's is: A progressive, incrementally-adoptable JavaScript framework for building UI on the web.

### What problem does it solve?

The one-liner description above doesn't clearly state what problem it solves.

For example, here is the introduction of an RPC project that made it to GitHub Trending today:

> Most machines on internet communicate with each other via TCP/IP. However TCP/IP only guarantees reliable data transmissions, we need to abstract more to build services:

![RPC Open Source Project](../img/rpc-example.png)

The above describes the problems this project solves, although the list of problems it solves is quite long, haha.

### What features does it have?

When we have several different frameworks like A, B, and C, as a developer, we need to compare their features. Here is an example of an MQTT implementation in Go:

![GO MQTT Example](../img/go-mqtt.png)

This project only supports Qos level 0. If the level we need is 1, then we can't use this project.

Another example is the lodash project:

> Lodash makes JavaScript easier by taking the hassle out of working with arrays,
numbers, objects, strings, etc. Lodash’s modular methods are great for:

 - Iterating arrays, objects, & strings
 - Manipulating & testing values
 - Creating composite functions

How would you write it? If you're thick-skinned enough, you could directly write a comparison with other projects, blabla:

![Comparison with other projects](../img/comparison.png)

Of course, you shouldn't overdo this, or you'll attract a lot of criticism.

### Installation and a hello, world example

After reading the introduction above, we should immediately follow with a hello, world example. Before running hello, world, we might need some additional installation steps, such as:

```
npm install koa
```

For example, Koa's example:

```
const Koa = require('koa');
const app = new Koa();

// response
app.use(ctx => {
  ctx.body = 'Hello Koa';
});

app.listen(3000);
```

As a programmer, you should understand its importance.

Fortunately, the installation here only has two steps, not like:

![Lan installation process](../img/lan-example.png)

For software that requires complex installation processes, the installation should be simplified, such as providing Docker images or directly providing a runnable Demo environment. To prevent users from giving up on using the library immediately after reading the README.

Technical Documentation
---

Alright, from a developer's perspective, if the above steps go smoothly, the next step is to use this open-source project to implement our features. At this point, we start shifting our attention to the documentation.

Previously, in a certain project, I encountered a big pitfall with third-party API documentation – the documentation only listed the API usage. Like the structure diagram generated by Intellij Idea below:

![API Example](../img/api-examples.png)

The documentation listed each function and the parameters each function needed. The information I got by directly decompiling the jar package using Intellij Idea was much more than what was in the documentation. The documentation had no examples, not even code on how to initialize the library.

WTF!

### Technical Documentation

For a complex open-source project, the documentation should detail the installation, compilation, configuration, etc., processes. As shown in the image below:

![Python Social Auth documentation](../img/python-social-auth-example.png)

And when we release a package, we need to keep repeating this process – if you use automated testing, then this process is automatically completed.

If our project is very simple to use, then we can just write some example code.

Furthermore, we can embed the documentation directly into the code. This can effectively reduce problems caused by documentation being out of sync.

![Lodash example](../img/lodash-code-example.png)

The above image is an example of Lodash using JSDoc.

Besides the examples above, we can also record some videos, write some articles explaining the project's thinking, architecture, etc.

### More Example Programs

Example code itself is part of the documentation; don't ask me why~~.

Anyway, besides a hello, world, you need examples for various scenarios:

![Redux](../img/redux-examples.png)

Without this many examples, dare you call yourself a user-friendly open-source project?

### Writing Technical Articles and Books

So far, we've done a series of markdown-related work, but it's not over yet. You know, only those who have actually written a series of open-source projects can truly appreciate what it means to be a markdown programmer~~.

Official documentation generally needs to describe processes in a relatively formal tone, which can be quite stifling. If you want a relaxed and humorous tone, you can write a series of technical articles. For instance, if this is a front-end framework, we can introduce how it works with a certain back-end framework; or a comparison with another framework, etc.

Alright, if everything goes smoothly, the next step is to attract more people to participate in the project.

Encouraging and Attracting Contributors
---

Attracting other developers to your project is not an easy task.

You need to constantly encourage them and help them solve problems in a timely manner to prevent them from giving up during the pull request process. This is particularly interesting. When a developer finds a bug in the project, they will try to solve it. At the same time, they will also bring a pull request to your project. But during this process, issues like testing might hinder their PR. At this point, we need to proactively guide/teach them what to do, or help them solve the remaining problems. Then, next time they submit a PR, they will be able to solve the problem.

This can be reflected in the README and introductions:

![Feel free to contribute!](../img/feel-free-to.png)

Even if it's just a PR to fix a typo, you can still merge it, ahaha~. Then, someone will help promote it, "I made a PR to the xxx project." When I first graduated, I also started with this type of PR~~.