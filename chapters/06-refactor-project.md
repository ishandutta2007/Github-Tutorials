# Improving GitHub Project Code Quality: Refactoring

Perhaps you already know what refactoring is, and you know what benefits it brings. When I first started learning refactoring and design patterns, I needed to find good examples to aid my learning. Sometimes I had to create better scenarios to implement these features.

One day, I realized I was repeatedly explaining certain topics, so I planned to put these essential skills on GitHub, which led to the [Artisan Stack](https://github.com/phodal-archive/artisanstack.github.io) project.

Every programmer is inevitably a Coder, but a Coder without well-mastered skills cannot be considered an Artisan. An Artisan needs creative methods.

## Why Refactor?

> For better code.

After more than a year of work, my main daily task was fixing bugs. At first, it seemed boring, but later I realized fixing bugs required better skills. Sometimes you might face piles of messy code; sometimes you might spend days reading code. Rewriting those few dozen lines of code might take less than a day. But if you can't understand why it was done that way in the first place, your changes will only introduce more bugs. Fixing bugs is more about maintaining code. As the old saying goes:

> Writing code is easy; reading code is hard.

Suppose writing that code takes half a day, but others need a full day to understand it. Why not spend a day writing the code so others can understand it in half a day or less?

If your code is already live, even if it's a mess, don't lightly attempt **refactoring without tests**.

Starting from the frontend is because the messiest and least testable code tends to be there.

Let's look at our first training challenge, which is quite challenging.

## Refactoring uMarkdown

Code and setup instructions can be found on GitHub: [js-refactor](https://github.com/artisanstack/js-refactor)

### Code Description

`uMarkdown` is a library for converting Markdown to HTML. The code looks like a typical procedural example:

```javascript
/* code */
while ((stra = micromarkdown.regexobject.code.exec(str)) !== null) {
  str = str.replace(stra[0], '<code>\n' + micromarkdown.htmlEncode(stra[1]).replace(/\n/gm, '<br/>').replace(/\ /gm, '&nbsp;') + '</code>\n');
}

/* headlines */
while ((stra = micromarkdown.regexobject.headline.exec(str)) !== null) {
  count = stra[1].length;
  str = str.replace(stra[0], '<h' + count + '>' + stra[2] + '</h' + count + '>' + '\n');
}

/* mail */
while ((stra = micromarkdown.regexobject.mail.exec(str)) !== null) {
  str = str.replace(stra[0], '<a href="mailto:' + stra[1] + '">' + stra[1] + '</a>');
}
```

Choosing this as the starting point for refactoring is not only because I did a lot of refactoring while writing [EchoesWorks](https://github.com/phodal/echoesworks) before, but also because it's well-suited for the theory of **refactoring to patterns**. Let's send a pull request to the author after we finish refactoring.

The Markdown parsing process is somewhat similar to the **Pipe and Filters** pattern (an architectural pattern).

Filters are the regular expression sets we see in the code:

```javascript
regexobject: {
    headline: /^(\#{1,6})([^\#\n]+)$/m,
    code: /\s\`\`\`\n?([^`]+)\`\`\`/g
```

They match corresponding Markdown types and then perform replacements and processing. The `str` variable serves as both the input and output of the pipeline.

Next, we can perform simple refactoring on it.

(PS: I recommend using WebStorm for refactoring; it has built-in refactoring features.)

As an example, let's first extract a `codeHandler` method. That is, transform the above

```javascript
/* code */
while ((stra = micromarkdown.regexobject.code.exec(str)) !== null) {
  str = str.replace(stra[0], '<code>\n' + micromarkdown.htmlEncode(stra[1]).replace(/\n/gm, '<br/>').replace(/\ /gm, '&nbsp;') + '</code>\n');
}
```

into an extracted method:

```javascript
codeFilter: function (str, stra) {
    return str.replace(stra[0], '<code>\n' + micromarkdown.htmlEncode(stra[1]).replace(/\n/gm, '<br/>').replace(/\ /gm, '&nbsp;') + '</code>\n');
  },    
```

The while statement then becomes:

```javascript
while ((stra = regexobject.code.exec(str)) !== null) {
    str = this.codeFilter(str, stra);
}
```

Then, run all the tests.

```
grunt test
```

Similarly, we can refactor the `mail`, `headline`, and other methods. It then becomes code similar to the following:

```javascript
/* code */
while ((execStr = regExpObject.code.exec(str)) !== null) {
str = codeHandler(str, execStr);
}

/* headlines */
while ((execStr = regExpObject.headline.exec(str)) !== null) {
str = headlineHandler(str, execStr);
}

/* lists */
while ((execStr = regExpObject.lists.exec(str)) !== null) {
str = listHandler(str, execStr);
}

/* tables */
while ((execStr = regExpObject.tables.exec(str)) !== null) {
str = tableHandler(str, execStr, strict);
}
```

Then you also see a bunch of duplicate code above. Next, let's use a JavaScript **trick**, the `apply` method, to turn the repetitive code into:

```javascript
['code', 'headline', 'lists', 'tables', 'links', 'mail', 'url', 'smlinks', 'hr'].forEach(function (type) {
    while ((stra = regexobject[type].exec(str)) !== null) {
        str = that[(type + 'Handler')].apply(that, [stra, str, strict]);
    }
});
```

Run the tests, blabla, all pass.

```javascript
 Markdown
   ✓ should parse h1~h3
   ✓ should parse link
   ✓ should special link
   ✓ should parse font style
   ✓ should parse code
   ✓ should parse ul list
   ✓ should parse ul table
   ✓ should return correctly class name
```

Come and try it: [https://github.com/artisanstack/js-refactor](https://github.com/artisanstack/js-refactor)

It's time to discuss this Refactoring powerhouse. I first saw this refactoring process from ThoughtWorks' Zheng Daye School, but previously I had a bad impression of Eclipse, another Java editor... That's not very important now. Try this editor, which is widely used in companies.

## Intellij Idea Refactoring

The development process generally looks like this; test-driven development is recommended.

    Write tests -> Write feature code -> Modify tests -> Refactor

Last time when chatting with a buddy, I learned that tests come after when features are simple, and come first when features are complex and you don't know where to start.

Before starting, please forgive my ignorance of some Java language aspects. Now, look at the Main function I wrote:

```java
package com.phodal.learing;

public class Main {

    public static void main(String[] args) {
        int c=new Cal().add(1,2);
        int d=new Cal2().sub(2,1);
        System.out.println("Hello,s");
        System.out.println(c);
        System.out.println(d);
    }
}
```

The code is written okay (self-assessment). Ignoring the Cal and Cal2 classes for now. Most of it is understandable, except that `c` and `d` don't clearly indicate their meaning. So...

### Rename

**Shortcut: Shift+F6**

**Purpose: Rename**

 - Place the cursor on `c` in `int c`, press Shift + F6, enter `result_add`
 - Move the cursor to `d` in `int d`, press Shift + F6, enter `result_sub`

Thus, we get:

```java
package com.phodal.learing;

public class Main {

    public static void main(String[] args) {
        int result_add=new Cal().add(1,2);
        int result_sub=new Cal2().sub(2,1);
        System.out.println("Hello,s");
        System.out.println(result_add);
        System.out.println(result_sub);
    }
}
```

### Extract Method

**Shortcut: Alt+command+m** (Mac) / **Ctrl+Alt+M** (Windows/Linux)

**Purpose: Extract Method**

- Select `System.out.println(result_add);`
- Press Alt + command + m (Mac) / Ctrl + Alt + M (Windows/Linux)
- In the pop-up window, enter `mprint`

Thus, we get:

```java
public static void main(String[] args) {
    int result_add=new Cal().add(1,2);
    int result_sub=new Cal2().sub(2,1);
    System.out.println("Hello,s");
    mprint(result_add);
    mprint(result_sub);
}

private static void mprint(int result_sub) {
    System.out.println(result_sub);
}
```

It seems we shouldn't treat `System.out.println` this way, so let's inline it back.

### Inline Method

**Shortcut: Alt + command + n** (Mac) / **Ctrl+Alt+N** (Windows/Linux)

**Purpose: Inline Method**

- Select `mprint` in main
- Alt + command + n (Mac) / Ctrl+Alt+N (Windows/Linux)
- Select "Inline all invocations and remove the method(2 occurrences)" and click OK

Then we have essentially done nothing~~:

```java
public static void main(String[] args) {
    int result_add=new Cal().add(1,2);
    int result_sub=new Cal2().sub(2,1);
    System.out.println("Hello,s");
    System.out.println(result_add);
    System.out.println(result_sub);
}
```

This example might not be great, but it's sufficient for illustration.

### Pull Members Up

Before starting, let's look at the Cal2 class:

```java
public class Cal2 extends Cal {

    public int sub(int a,int b){
        return a-b;
    }
}
```

And its parent class Cal:

```java
public class Cal {

    public int add(int a,int b){
        return a+b;
    }

}
```

The final result is moving the `sub` method from the Cal2 class to the parent class:

```java
public class Cal {

    public int add(int a,int b){
        return a+b;
    }

    public int sub(int a,int b){
        return a-b;
    }
}
```

All we need to do is right-click.

### Refactoring: Replace Temp with Query

Shortcut:

Mac: None

Windows/Linux: None

Or: `Shift` + `Alt` + `command` + `T` (Mac) / `Ctrl`+`Alt`+`Shift`+`T` (Windows/Linux), then select `Replace Temp with Query`

Mouse: **Refactor** | `Replace Temp with Query`

#### Before Refactoring

Too many temporary variables can lead to longer functions. Functions shouldn't be too long to keep them single-purpose. This is another goal of refactoring; only when a function focuses on its task is it easier to read.

Take the code from the book as an example:

```java
import java.lang.System;

public class replaceTemp {
    public void count() {
        double basePrice = _quantity * _itemPrice;
        if (basePrice > 1000) {
            return basePrice * 0.95;
        } else {
            return basePrice * 0.98;
        }
    }
}
```

#### Refactoring

Select `basePrice` and happily click the refactor menu above.

![Replace Temp With Query](../img/replace.jpg)

It returns:

```java
import java.lang.System;

public class replaceTemp {
    public void count() {
        if (basePrice() > 1000) {
            return basePrice() * 0.95;
        } else {
            return basePrice() * 0.98;
        }
    }

    private double basePrice() {
        return _quantity * _itemPrice;
    }
}
```

Actually, we could also:

1.  Select `_quantity * _itemPrice`
2.  Perform `Extract Method` on it
3.  Select `basePrice` and then `Inline Method`

#### Intellij IDEA Refactoring

In Intellij IDEA's documentation, the example is like this:

```java
public class replaceTemp {

    public void method() {
        String str = "str";
        String aString = returnString().concat(str);
        System.out.println(aString);
    }

}
```

Then we select `aString`, open the refactor menu, or press

`Command`+`Alt`+`Shift`+`T` (Mac) / `Ctrl`+`Alt`+`Shift`+`T` (Windows/Linux) and select Replace Temp with Query

We get the following result:

```java
import java.lang.String;

public class replaceTemp {

    public void method() {
        String str = "str";
        System.out.println(aString(str));
    }

    private String aString(String str) {
        return returnString().concat(str);
    }

}
```