Creating Open Source Projects
===

People create open source projects for different reasons, but regardless of the purpose, the process is generally the same.

1.  First, we need to come up with a name for our project.
2.  Then, choose a suitable LICENSE for our open source project.
3.  Then, proceed to create the project.

Choosing a Good Name
---

Naming things has never been easy.

Therefore, I'll keep it brief: usually, it's about choosing a meaningful name, but having no specific meaning is perfectly fine too.

Often, if you plan to have a series of open source projects, it's good to maintain a certain naming convention.

Picking the Right LICENSE
---

> In the late 1970s and early 1980s, to prevent their software from being used by competitors, most vendors stopped distributing their software's source code and began using copyrights and restrictive software licenses to limit or prohibit copying or redistribution of the source code. Subsequently, Richard Matthew Stallman initiated the free software movement. He pioneered the concept of Copyleft: using the principles of copyright law to protect the rights to use, modify, and distribute free software, and was a primary author of free software licenses describing these terms. The most well-known is the GPL (a widely used free software license).[^rms]

(PS: For more information and history about free software and RMS, you can read "Free as in Freedom: Richard Stallman's Crusade for Free Software.")

[^rms]: https://en.wikipedia.org/wiki/Richard_Stallman

Later, the concept of open source software was born. The requirements for open source are somewhat looser than those for free software[^gnu_gpl]. All free software source code released to date is open source software, but not all open source software is free software. This is because different licenses grant users different rights. For example, the GPL license mandates that modified code must also be open-sourced, whereas the more permissive MIT license has no such requirement.

[^gnu_gpl]: https://www.gnu.org/philosophy/open-source-misses-the-point.en.html

The chart below shows the market share and usage of different open source licenses.

![License Usage](../img/permissive-vs-copylift-license-2.jpg)

Also, for example, in some foreign books that include code, the author usually states the copyright of the book's code in the preface or a similar section. Such as:

> You may need to use the code from this book in your own program or document, but unless you're using large portions, you generally don't need to contact us for permission. For instance, writing a program using a few code snippets from this book doesn't require permission, etc.

Thus, choosing an appropriate LICENSE becomes an interesting topic. For this purpose, I've created a flowchart on how to select an open source license:

[![How to Choose a License](../img/licenses.png)](https://github.com/phodal/licenses)

Simply put, these Licenses differ in the rights they grant. For example, placing code in the Public Domain means anyone can modify it and does not need to attribute the original author. However, if you want others to attribute you as the author, you would need the MIT license. If you want to allow others to use your code in closed-source projects, you might consider the MPL license, and so on.

Now, let's briefly introduce a few different licenses.

### Public Domain

> WTFPL (Do What The Fuck You Want To Public License) is a rarely used, extremely permissive free software license. Its terms are essentially equivalent to dedicating the work to the public domain.[^wtfpl]

[^wtfpl]: https://en.wikipedia.org/wiki/WTFPL

This means that anyone who obtains this code can modify it however they wish.

### GPL

Due to the "copyleft" nature of the GPL, it means that when others use our code, their derived code must also be licensed under the GPL and made open source. That is: the GPL is a "viral" or "infectious" license, as its terms stipulate that derivative works must also be GPL-licensed.

If our goal is to allow others to use a library without requiring their own code to be open-sourced, we might use the LGPL. However, modifying the library itself is a different case.

### MIT

Therefore, generally speaking, I use the MIT license. At the very least, I retain attribution rights, meaning you can modify my code, but you must include my name in the LICENSE file.

Choosing MIT is particularly interesting, especially in recent years, where incidents have occurred, such as:

 *   [The iView "plagiarizing" Element UI incident](https://zhuanlan.zhihu.com/p/25739512)
 *   [The AndroidTVLauncher "plagiarizing" incident](https://github.com/JackyAndroid/AndroidTVLauncher/issues/22)

And so on. This teaches us that if you don't want to have such experiences, then maybe don't use MIT.

### Creative Commons

Yes, when I write in Markdown, considering that it might be published as a physical book in the future, I use the CC-BY-NC-ND license:

 *   CC -> Creative Commons
 *   BY -> Attribution
 *   NC -> NonCommercial
 *   ND -> NoDerivatives.

This means anyone is free to copy, distribute, display, and perform my e-book, but not for commercial purposes (the author themselves can). They can freely post it on their blog or in various articles. However, they must attribute the original source and are not allowed to alter, transform, or build upon the work.

If you don't mind, you can use the Public Domain. But if you do that, one day, if someone directly publishes your work as a book, you might be quite frustrated.