GitHub Streak
===

## 100 Days

I've been quite diligent. Although I originally thought of just maintaining a streak of 100~200 days on GitHub, reaching today's point is still pretty good.

![Longest Streak](../img/longest-streak.png)

``In the process of constantly reinventing the wheel, I also keep building cars.``

Before that article about a 365-day streak appeared, a senior at our company ([https://github.com/dreamhead](https://github.com/dreamhead)) had also mentioned internally about committing every day. Of course, that wasn't my motivation. Before the 140-day streak:

- I had created pull requests for projects like Google's `ngx_speed`, `node-coap`, etc.
- There were also projects like `free-programming-books`, `free-programming-books-zh_CN`.
- And of course, there was a previous 20-day streak.

Comparing my commits to the 365-day streak's commits, I found my total was nearly 0.5 times more.

![365 Streak](../img/365-streak.jpg)

This also seems to imply that my average daily commit count was much higher compared to theirs.

During the 20-day streak, there was this problem: *committing code just for the sake of committing*, which I eventually gave up.

Now it's `committing to fill in pits`, as I've dug too many ideas for myself.

### Improvement in 40 Days

At that time, I needed to go to India for graduate training, for about 5 weeks. I thought I couldn't come back empty-handed. So, after National Day ended, I had my first commit. I had just returned from a trip and thought about having photos from different places. So the repo was named [onmap](https://github.com/phodal/onmap) – displaying my photos on a map at their shooting locations (phone was Lumia 920). However, I lost the streak due to an account change in the middle.

Let's start from India. At that time, I mainly maintained three repos:

- IoT CoAP protocol
- The e-book [Step-by-Step IoT System Design](https://github.com/phodal/designiot)
- A Node.js + JS website

Let's talk about the last one. The last one was a practice project. Because the training was quite boring, there was a lot of free time. My English wasn't good, and I couldn't understand the Indians well. Evenings were basically spent writing code silently at my accommodation, so the goals at that time were:

- TDD
- Test coverage
- Clean code

That's why that repo has this line:

![Repo Status](../img/repo-status.png)

Achieving 98% coverage was quite an effort. Of course, Code Climate also reached 4.0, and there were 112 commits. This also brought some improvements:

- Improved code quality (Code Climate focuses more on duplicate code and other bad smells than jslint).
- Better grasp of Mock, Stub, FakeServer, etc.
- Ability to continuously deliver software (version management, automated testing, CI, deployment, etc.)

### The 100-Day Challenge

(PS: After returning from India, since my girlfriend was interning in Thailand, I had more time to read books and write code.)

Interestingly, the further into the middle period, the number of commits increased. Besides some simple pull requests, some new wheels (projects) also appeared.

![Problem](../img/problem.jpg)

This is the commits from last week, which means within a week, I had to switch between 8 repos. And now I have a new idea, and I discovered a bunch of problems:

 - Working on one repo today, suddenly finding an issue on another repo that needs fixing, so I put down the current code.
 - Switching between different repos easily disperses focus.
 - It's easy to find too many features that could be implemented, but time is limited.
 - Not enough free time except on weekends.
 - Hoping to find interested people, but then realizing there isn't that much time to look for people.

### Hopes for 140 Days

After experiencing 100 days, it seems the whole person has relaxed a bit, after all, the goal was 100~200 days. Up to now, it seems there won't be any special sentiment, except for some hopes.

Of course, for an open-source project author, it's best to have the following situations:

- Many people know about the project.
- Many people use the project.
- The project is mentioned in places where it can quickly solve problems.
- Bugs, issues, problems are reported.
- Bugs are reported and fixed. (PS: This is the ideal situation.)

## 200 Days Showcase

Today is my 200th consecutive day on GitHub, and I'm quite happy to have reached it:

![GitHub 200 days](../img/github-200-days.png)

The background story: After National Day last year, I went to India for graduate training – that magical country. But before going, I had already been on the project for over nine months, and the challenges on the project were decreasing. Time in India was relatively plentiful. So I set a long-term goal for myself: a 100~200 day longest streak.

Perhaps you've seen an article before [Let's Streak](https://github.com/phodal/github-roam/blob/master/chapters/12-streak-your-github.md). That was already at 140 days, but I was still muddle-headed. By today, a clearer thought process has gradually emerged.

Let's have a ShowCase first, and then... next article we'll continue.

### Brief Description of Some Projects

The training mentioned above initially involved a website written in Java, with automated testing, CI, CD, etc. Due to internal team training, the code couldn't be made public, and other factors, plus it was boring. I conveniently made a Server with Node.js + RESTify, and the front-end logic with Backbone + RequireJS + jQuery. So during that time, I was also maintaining some old repos, like [iot-coap](https://github.com/phodal/iot-coap), [iot](https://github.com/phodal/iot). The former is the repo for which I got the WebStorm open-source License, the latter was my graduation project.

For such a project, it also needed testing, automated testing, CI, etc. CI used Travis-CI. The overall tech stack was as follows:

#### Tech Stack

Front-end:

- Backbone
- RequireJS
- Underscore
- Mustache
- Pure CSS

Back-end:

- RESTify

Testing:

- Jasmine
- Chai
- Sinon
- Mocha
- Jasmine-jQuery

I kept writing until the five-week training ended, just without automatic deployment. Thinking about it, projects that could use github-page would be nice~~.

There were also some interesting small projects during the process, like:

### Google Maps solr polygon search

[Google Maps solr polygon search](http://www.phodal.com/blog/google-map-width-solr-use-polygon-search/)

![Google Maps solr](../img/solr.png)

Code: [https://github.com/phodal/gmap-solr](https://github.com/phodal/gmap-solr)

### Skill Tree

This can be told in two parts:

#### Refactoring Skill Tree

The original used:

- Knockout
- RequireJS
- jQuery
- Gulp

![Skill Tree](../img/skilltree.jpg)

Code: [https://github.com/phodal/skillock](https://github.com/phodal/skillock)

#### Skill Tree Sherlock

- D3.js
- Dagre-D3.js
- jquery.tooltipster.js
- jQuery
- Lettuce
- Knockout.js
- Require.js

![Sherlock skill tree](../img/sherlock.png)

Code: [https://github.com/phodal/sherlock](https://github.com/phodal/sherlock)

#### Django Ionic ElasticSearch Map Search

![Django Elastic Search](../img/elasticsearch_ionit_map.jpg)

- ElasticSearch
- Django
- Ionic
- OpenLayers 3

Code: [https://github.com/phodal/django-elasticsearch](https://github.com/phodal/django-elasticsearch)

#### Resume Generator

![Resume](../img/resume.png)

- React
- jsPDF
- jQuery
- RequireJS
- Showdown

Code: [https://github.com/phodal/resume](https://github.com/phodal/resume)


#### Nginx Big Data Learning

![Nginx Pig](../img/nginx_pig.jpg)

- ElasticSearch
- Hadoop
- Pig

Code: [https://github.com/phodal/learning-data/tree/master/nginx](https://github.com/phodal/learning-data/tree/master/nginx)

#### Others

Although the tech stack mainly focuses on Python, JavaScript, there are also some Ruby, Pig, Shell, Java code, but I'm still more accustomed to Python and JavaScript. Some frameworks I found useful:

- Ionic: Start Hybrid mobile apps.
- Django: Python Web development powerhouse.
- Flask: Python Web development pocket knife.
- RequireJS: Manage JS dependencies.
- Backbone: Model + View + Router.
- Angular: ...
- Knockout: MVV*.
- React: Said to be hot.
- Cordova: Foundation for Hybrid apps.

There should also be:

- ElasticSearch
- Solr
- Hadoop
- Pig
- MongoDB
- Redis

## 365 Days

> Given a year, how would you improve your skills???

![GitHub 365](../img/github-365.jpg)

Taking advantage of this rare sick leave (cursed air), I'll write an article to commemorate the past 366 days. Although I thought about writing a sustainable open-source framework this year, that ultimately depends on a good idea. On my [GitHub Incubator](http://github.com/phodal/ideas) page, there doesn't seem to be a particularly satisfying idea, although there are various interesting ideas. Most were completed in the past year, but some haven't been done yet.

Although continuously streaking on GitHub may seem unnecessary, people always need some pursuit. If you are aimless but want to improve your skills, why not try? After all, very few people are naturally very skilled without much practice; such people don't seem to exist. Most people reach what others call "good skills" only after practice.

This reminds me of some questions on the opinion-filled Zhihu. In topics where IQ seems completely outmatched, it's always because those people learned earlier – where does genius come from? So-called geniuses should be like future intelligent life, knowing everything at birth. If not, it just means their practice was thorough.

Inadequate practice means even if you practice twice the 10,000 hours, it's useless. If you learn later than others, losing to others for **a very long time** (possibly until you're in a coffin) is inevitable – lagging behind leaves you vulnerable. Just like I graduated from a school at the bottom of the second-tier. If in the past, I always maintained the same learning speed as others (from various key schools), then I could only be a Loser.

It's important to note that for you, getting into a second-tier university was hard, not because you're less intelligent. Unequal distribution of educational resources has, to some extent, led to the emergence of a new class system. As [my homepage](https://www.phodal.com/) says: **THE ONLY FAIR IS NOT FAIR**. There's still a lot we can do – **CREATE & SHARE**. The real misfortune is educational problems caused by malnutrition.

So, after thinking through many things, I came up with the Re-Practise plan, and the 365-day streak is just one product of it.

### Basic Programming Ability

Although algorithms are important, coding is the foundational skill. Algorithms and programming are somewhat different fields; algorithmic programming is a level above programming. No matter how well you write algorithms, if others find it hard to reuse directly, in their eyes it's shit. Coming up with code that works is simple; learning to refactor it to make it more readable is meaningful.

So, at a certain moment, I created an organization on GitHub called [Artisan Stack](https://github.com/artisanstack). At that time, I wanted to find some JavaScript projects on GitHub and refactor their code. But after all, influence wasn't enough, participation was low.

#### Refactoring

If you know how to write highly readable code, then I think you don't need this, but this means you spend more time thinking. When talking about refactoring, it reminds me of TDD (Test-Driven Development). Even if not TDD, if you're writing tests, then you can refactor. (I previously wrote some articles on refactoring with Intellij IDEA: [Extract Method](https://www.phodal.com/blog/intellij-idea-refactor-extract-method/), [Replace Temp with Query](https://www.phodal.com/blog/intellij-idea-refactor-replace-temp-with-query/), [Refactoring and Intellij Idea Primer](https://www.phodal.com/blog/thoughtworks-refactor-and-intellij-idea/), [Inline Method](https://www.phodal.com/blog/intellij-idea-refactor-inline-method/).)

In various articles, we've seen some related content; the best reference is the book "Refactoring." The most basic principle is function naming. Naming is hard; naming something others can understand is even harder. Others include long functions, oversized classes, duplicate code, etc. In my limited experience interviewing others, these are the most common issues.

#### Testing

Without testing, everything else is nonsense. Writing good tests is hard; writing a test is relatively easy. But sometimes we write tests just for the sake of testing.

While writing [EchoesWorks](https://github.com/echoesworks/echoesworks) and [Lan](https://github.com/phodal/lan), I tried to ensure sufficient test coverage.

![lan](../img/lan.png)

![EchoesWorks](../img/echoesworks.png)

Starting with TDD ensures methods are testable. Going from feature to testing can improve work efficiency, but only makes tests become tests, not part of the code.

Testing is the last mile of code. So, try to add tests to your projects on GitHub.

#### The Coding Process

When I first joined TW, while Pairing, someone always taught me how to start coding; this should also be a basic skill. Combining daily life, let's reenact this process:

1.  Have a measurable, achievable, process-testable goal.
2.  Tasking (i.e., breaking down the process to achieve the goal).
3.  Implement step by step (e.g., TDD).
4.  Achieve the goal.

Applying to the current scenario:

1.  I want to streak for 365 days on GitHub. Corresponding to each time period, the goal should be measurable, testable – i.e., daily Contributions.
2.  Breaking it down is a painful process. Ideally, we should have daily commits, but this depends on your number of repos. Without new ideas, this becomes committing just for Contributions.
3.  Implement step by step.

In our actual work, it's similar: receive a task, break it down, complete it step by step. However, implementation is slightly more complex because tasks always have contention and priorities.

### Technology and Framework Design

In the blog post before last, "[After 500：写了第 500 篇博客，然后呢？](https://www.phodal.com/blog/after-500-blogposts-analytics-after-tech/)" I also deeply discussed this issue. Technology has always favored latecomers. For technical personnel, it's the same; latecomers hold a big advantage.

If we only focus our attention solely on technology, then we have no advantage. Relying on our programming experience, we can create some frameworks at specific times. And architectural design itself is interesting, probably because programmers love to create. (PS: I previously wrote an article, "[对不起，我并不热爱编程，我只喜欢创造](https://www.phodal.com/blog/sorry-i-don't-like-programming/)").

**Creation is a process of re-mastering knowledge.**

Looking back at writing echoesworks, initially I needed a web-based PPT. Of course, there were already many such things, like impress.js, bespoke.js, etc. Analyzing the needed features: markdown parser, keyboard event handling, Ajax, progress bar display, image processing, Slide. We can find various modules on GitHub. What we need to do is combine them. Before that, I tried using similar principles to write (assemble) [Lettuce](https://github.com/phodal/lettuce).

Combination is a more challenging process than creation. We need to design glue in this process to stick these pieces of code together and eventually make it work. This is similar to the task division we encounter daily: each person is responsible for a corresponding module, and finally integration.

When I wrote [lan](https://github.com/phodal/lan), it was similar, but the difference was I had already designed a clear architecture diagram.

![Lan IoT](../img/lan-iot.jpg)

And our implementation coding process is also like this, using different frameworks and making them work. Like the early [moqi.mobi](https://github.com/echoesworks/moqi.mobi), based on Backbone, RequireJS, Underscore, Mustache, Pure CSS. Later, replacing the View layer with React, there was the [backbone-react](https://github.com/phodal/backbone-react) practice.

Technology, like people, needs to constantly advance to a higher level. We just need to keep Re-Practising.

### Domain and Practice

Talking about business might not suit programmers' taste, so let's say domain. People from different industries, like Baidu, Alibaba, Tencent, their core domains are different.

And domains themselves are similar. This explains why internet companies like to poach from each other but generally don't poach from non-internet domains like Huawei, ZTE, etc. Outside your domain, you might not even be as good as a graduate. Domain, business, like technology, is a process of continuously strengthening knowledge. Ritchie first implemented the BCPL language, then designed the C language, and the BCPL language was initially based on the CPL language.

The domain itself is also constantly evolving.

This is also the next area worth improving.

### Others

It's time to write this summary. Going from not knowing how to code to coding is a process from 0 to 1, but going from 1 to 60 isn't easy. Whether it's grinding GitHub (not automatic commits) or changing jobs, we are constantly practicing.

And practice should be divided into several steps, not limited to technology:

1.  Coding
2.  Architecture
3.  Design
4.  ...

---

## 500 Days

Although there have been articles for 100 days, 200 days, and 365 days, this is not a symbolic 500-day article. People have different opinions on such a thing. Some will say it's a good thing, others not. But others' opinions ultimately don't matter, because only you know yourself. Others only offer perspectives from their angle.

In these 500 days, I discovered two interesting things, only realizing them when summarizing:

1.  The emotional cycle of programming
2.  Deliberate practice

So, when we practice continuously, we can write better code.

I think you've also heard of the 10,000-hour rule: to become an expert in a field requires 10,000 hours. The most important point in this is deliberate practice – not just repeatedly writing the same algorithm in different languages. If we have 8 hours of work time + 2 hours of improvement time per day, then we still need 1000 days to reach 10,000 hours.

### 500 Days and 10,000 Hours

Of course, if you even write code in your dreams, then I think 500 days is enough, haha~~.

![Gtihub 500](../img/github-500.jpg)

Although not the longest streak, according to [Most active GitHub users ](http://git.io/top), it seems I'm the person with the most commits from mainland China, bar none. Considering the commits are meaningful – not machine-generated, not consciously farming – I feel a great sense of achievement.

Two important points to achieve a 500-day streak are: time and ideas. But I think ideas aren't very important; we can build wheels, which is what I did most in the early days, constantly building wheels – as mentioned in the article "[造轮子与从Github生成轮子](https://www.phodal.com/blog/create-framework-from-github/)". Besides, you can also "[GitHub去管理你的idea](https://www.phodal.com/blog/use-github-manage-idea/)", every time you think of an Idea and complete an idea, you get more commits.

Time is ironic because people have to work overtime. The reasons for overtime are either because the work content is interesting or because of money. If not for money, why not change jobs? Like my company. There seems to be a lot of opposition between the two, but I always think that skill improvement can solve income problems later, without relying on overtime to solve it. People have to live; money is necessary, but programmers' incomes aren't low.

### The Emotional Cycle of Programming

Then, I observed some interesting phenomena – the emotional cycle of programming is also quite obvious.

> The so-called "emotional cycle" refers to the time it takes for a person's emotional highs and lows to alternate.

The emotional cycle is as shown below:

![情绪周期](../img/qingxu.jpg)

Simply put, **there are periods when writing code feels super satisfying, and periods when you don't want to write code**. But if you put it another way: **there are periods when reading books, writing documentation feels great, and periods when you don't feel like reading books or writing documentation**. That's why the green squares on my GitHub homepage are all sorts of patterns. However, due to the "IoT Weekly", I regularly update a related open-source project.

But overall, I'm used to building some wheels and creating documentation at certain times, which is why my GitHub has some open-source e-books.

### Deliberate Practice

Programming requires a long learning time and a long practice time. Although I started programming in elementary school and consider myself quite talented, breaking through the last threshold still took three or four years. A big part of the reason was not finding a suitable direction. During that time, I didn't practice well. Later, realizing I would encounter the next threshold, I began to try deliberate practice.

When I started working, I wrote an article titled "[重新思考工作](https://www.phodal.com/blog/rethink-about-the-work/)". In the article, I mentioned several practice points:

 - Improve coding accuracy.
 - Write cleaner code.
 - Spoken English (foreign company).
 - Targeted language skill enhancement.

After practicing for some days, I found this still too boring. I naturally like interesting things; fun brings more passion~~. However, typing practice like the image below is quite interesting:

![Typing Practice](../img/huovd.png)

Still, I typed a bunch of wrong characters. But compared to most people, it's not bad, at least touch typing. But there's still a lot of room for improvement.

Later, I started some incorrect practices, like practicing design patterns and architectures. Trying to practice design patterns not used in production, and some architectural patterns. This meant forcing some design patterns. Finally, I started practicing with projects as the goal, which is why my GitHub commit count is so high.

### Predictive Practice

Another interesting practice is work-oriented practice. When we foresee that our project will need certain technologies, we might adopt certain technologies in the future, so we need to start predictively practicing these technologies.

The good thing is: these projects might be popular with beginners in the future.

### Summary

Everyone has their own direction, a good development path; sharing and creating are both good paths.

THE ONLY FAIR IS NOT FAIR. ENJOY CREATE & SHARE.

## Within 365*2-7 Days

Just after graduation, for a period, I was always confused about how to improve coding ability – because what I did on projects often wasn't what I wanted. I thought about finding some interesting things to do for fun, practicing skills along the way.

> If you know your coding ability is insufficient, why not spend two years improving it?

### Coding Practice

Coding is something worth practicing. The programming experts you see in books and on the internet all accumulated from little skills. Early exposure gives you a good start, and good practice helps you advance better.

I remember when I first started practicing, I divided it into several stages:

 - Following the book "Refactoring: Improving the Design of Existing Code", I looked for code with bad smells and tried to make the code elegant.
 - Following "Design Patterns" and "Refactoring to Patterns", I refactored code into certain design patterns.
 - Following "Pattern-Oriented Software Architecture", I designed some software architectures.

These aren't easy. Often, there are some patterns we don't have good practice with. But these things aren't meant to be rigidly applied. We need to know these things exist, so that one day, we can retrieve this knowledge from our repository.

![10000 hours](../img/10000.png)

Our deliberate practice combined with perseverance always leads to significant progress. But before we practice, you need a goal. This goal can be an Idea, a design pattern, an imitation, etc. These can all be well-managed as Issues.

In the first few days we set the goal, we can easily do it. Similarly, we can easily reach 21 days. But we easily lose some goals after 21 days. So before starting practice, you need to create a list to help improve your skills, then gradually improve. For example:

1.  Try using React + Redux + Koa 2, or Angular 2 + TypeScript, so we can learn new technologies.
2.  Try designing a CMS using CQRS architecture, so we can practice architectural abilities.

When we think of a skill we can practice, it becomes something that can be managed as an Issue, and we can improve specifically.

Usually in this situation, we know what we don't know. When we are in a state of not knowing what we don't know, or not knowing what we know, then we need various online skill maps – like StuQ's skill maps.

![skilmap](../img/skillmap.png)

Then understand each item on the map, try to build your own system based on it – to move yourself from not knowing what you don't know, and then we can expand practice based on that.

Suggest trying our Growth, address: http://growth.ren.

The rest of the article lets me share: in these 723 days, what interesting things have I created (PS: let me show off a bit) – actually, I'm not just good at Markdown.

#### 2014

Time: 2014.10.08-2014.12.30

![2014.png](../img/2014.png)

During this period, most of the projects I created were IoT-related:

 - [iot-coap](https://github.com/phodal/iot-coap) An IoT project based on the CoAP protocol.
 - [designiot](https://github.com/phodal/designiot) The e-book "Teach You to Design IoT Systems".
 - [iot-document](https://github.com/phodal/awesome-iot-document) Collecting IoT-related materials, different from Awesome in nature.
 - [iot](https://github.com/phodal/iot) IoT based on the PHP framework Laravel.
 - iot-android An Android program matching the iot project.
 - etc.

It was these IoT projects that got Packt Publishing to contact me, leading to later dealings with domestic and foreign publishers. It also started various stories of technical reviewing, translation, and book writing. Thinking about it, this beginning was really good.

I also created a very interesting Chrome plugin during this time, called onebuttonapp – yes, imitating Amazon's one-click ordering. The purpose of this plugin was to verify that the Backbone, Require.js set I used on the project could work well in a plugin.

The OnMap project was created to display photos I took with my Nokia Lumia 920 on a map.

Of course, there were other small projects too.

#### 2015

![2015.png](../img/2015.png)

The entire interval was grinding various front-end tech stacks, creating various interesting projects:

 - [Lettuce Framework](https://github.com/phodal/lettuce), a simple SPA framework.
 - [echoesworks](https://github.com/phodal/echoesworks), a Slide framework supporting subtitles, Markdown, animations.
 - [diaonan](https://github.com/phodal/diaonan), an IoT project supporting CoAP, MQTT, HTTP.
 - [developer](https://github.com/phodal/developer), collecting various Web Developer growth roadmaps and reading maps.

During this time, I also created several hybrid app projects:

  - [learning-ionic](https://github.com/phodal/learning-ionic), programming language expert, various hello, world small apps.
  - [ionic-elasticsearch](https://github.com/phodal/ionic-elasticsearch), Django ElasticSearch Ionic building GIS mobile apps.
  - [designiot-app](https://github.com/phodal/designiot-app), Teach You to Design IoT App version.

More content can be seen in my Idea list: [https://github.com/phodal/ideas](https://github.com/phodal/ideas). I really don't want to write more.

#### 2016

![2016.png](../img/2016.png)

We have the Growth series of e-books, App, and Mole, a few highly representative projects are enough.

 - [Growth](https://github.com/phodal/growth), an app focusing on the growth of Web developers, covering the Web development process and tech stack, Web development learning paths, growth measurement, etc.
 - [Growth: Full-Stack Growth Engineer Guide](https://github.com/phodal/growth-ebook), a guide on how to become a full-stack growth engineer.
 - [Growth: Full-Stack Growth Engineer in Action](https://github.com/phodal/growth-in-action), Growth introduces a series of practices, while Growth in Action leads readers to perform these practices.

### See you Again

Stopping this streak is just for a better start.

If you also want to improve yourself, why not start by creating your ideas project, like my [Ideas](https://github.com/phodal/ideas) project, which already has a lot of Ideas. Then, based on these projects, we can create an e-book, i.e., [ideabook](https://github.com/phodal/ideabook).