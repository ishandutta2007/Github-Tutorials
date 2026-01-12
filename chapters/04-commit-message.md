Git Commit Messages and Several Different Standards
===

> Due to the impact of Growth 3.0 development, the frequency of article updates will be somewhat lower recently. Today, let's talk about how a good Git, SVN commit message is standardized.

In teamwork, using version control tools like Git and SVN is almost the industry standard. When we commit code, we need to write a commit message.

The primary purpose of a commit message is: **to tell people involved in the project what was done in this code commit**. For example, if I updated the version of React Native Elements, it could be: `[T] upgrade react native elements`. The corresponding code I modified would be files in `package.json` and `yarn.lock`. Generally, it is recommended to **commit in small steps**, meaning commits corresponding to each step of your Tasking process, with a commit message for each small step. The main purpose of this is: **to prevent modifying too many files in a single commit, leading to difficulties in future modifications, maintenance, rollbacks, etc.**

Different teams follow certain conventions. This article will mainly introduce the following styles:

 - Work style
 - Conventional style
 - Open-source library style

So, let's start with the practice I'm used to.

Work Style
---

In my first project, we used Jira as a kanban tool, Bamboo as the continuous integration server, and employed pair programming.

In Jira, every feature card has a corresponding card number, and Bamboo supports linking with Jira task card numbers. That is, the continuous integration server can display the corresponding task card number and the submitter.

Therefore, at that time, our standard was somewhat special:

```
[Task Card Number] xx & xx: do something 
```

For example: `[PHODAL-0001] ladohp & phodal: update documents`, explained as follows:

 - `PHODAL-0001`: the business task card number. It helps us trace the reason for a business modification, i.e., locate the source of a corresponding bug.
 - `ladohp & phodal`: the names of the two people in pair programming. The latter (phodal) is usually the one writing the code, and out of courtesy, it's placed last. Since Git only shows one author per commit, both names are written. When the committer is unavailable, the other person can be asked about the change.
 - `update documents`: what we did.

Disadvantage: For teams using kanban, there is no such thing as a task card number, so an additional practice is needed.

Conventional Style
---

For me personally, I am accustomed to this style:

```
[Task Category] Main Modified Component (Optional): Modification Content
```

Example 1: `[T] tabs: add icons`. Here, `T` indicates it's a technical card, `tabs` indicates the Tabs component was modified, and `add icons` means icons were added.

Example 2: `[SkillTree] detail: add link data`. Here, `SkillTree` indicates modifications under the SkillTree Tab, `detail` indicates the detail page was modified, and `add link data` means skill data was added.

The main reason for doing this is that it can easily help me **filter content related to specific business areas**.

Disadvantage: Achieving team consensus requires some extra cost.

Open-source Application, Open-source Library Style
---

Slightly different from our daily work: Release plans in work are usually scheduled in advance and don't require things like CHANGELOGs. Open-source applications and libraries need corresponding CHANGELOGs stating what features were added, what was modified, etc. After all, many things are maintained by the community.

Therefore, let's take the well-maintained open-source project Angular as an example. The Angular team recommends the following format:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

For instance, in `docs(changelog): update change log to beta.5`:

 - docs corresponds to the type of change.
 - changelog is the scope affected.
 - subject is the action performed.

Corresponding types include:

 - build: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
 - ci: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
 - docs: Documentation only changes
 - feat: A new feature
 - fix: A bug fix
 - perf: A code change that improves performance
 - refactor: A code change that neither fixes a bug nor adds a feature
 - style: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc.)
 - test: Adding missing tests or correcting existing tests

There are also 20+ corresponding Scopes. One could say this style of commit is more challenging than the ones above.

(Thanks to Google Translate for the quick translation support for the above 10 types.)

The advantage of this approach is that it can easily generate a CHANGELOG. There is also a specification called `Conventional Commits` which recommends a similar format.