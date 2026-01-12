How to "Find Inspiration (fork)" on GitHub
===

> Reinventing the wheel is recreating an existing or already optimized basic method by others.

Recently, I got the idea to write a game engine, after previously wanting to make a JavaScript front-end framework. Let's see how this line of thinking developed.

## Lettuce Building Process

> Lettuce is a minimalist mobile development framework.

The starting point of the story was this: "I wrote a lot of code, used frameworks, and in the end, I didn't know what I gained." Indeed, after working on some projects, I felt like I didn't gain anything substantial in the end. So, I thought about creating a framework.

### Requirements

There were several premises:

 - Why do I have to introduce such a heavy library like jQuery when I only need the selector and Ajax functions?
 - Why, when I just need a Template, do I think of using Mustache?
 - Why, when I need a Router, do I consider using Backbone?
 - Why, when all I need is an `isObject` function, do I resort to the entire Underscore library?

What I want is just a simple function, and I don't want to introduce a huge library. In other words, I need small parts from different libraries, not a whole library.

Essentially, what I wanted was:

> Build a library that extracts different functions from various libraries.

### Plan

At this point, I referenced an e-book "Build JavaScript Framework," combined with some usual needs, so I quickly knew what features I needed:

 - Promise support
 - Class (PS: there wasn't a good way to use classes)
 - Template: a simple template engine
 - Router: to control page routing
 - Ajax: basic Ajax Get/Post requests

When working on some practical projects, I also encountered the need for these features:

 - Effect: simple page effects
 - AMD support

And we had a premise to keep this library as small as possible, while also needing tests.

### Implementing the First Requirement

Let's briefly talk about how to implement a simple requirement.

#### Generating the Framework

Since Yeoman can generate a simple skeleton, we can use it to generate the project's basic structure.

 - Gulp
 - Jasmine

#### Searching

I searched on GitHub and saw the following results:

- [https://github.com/then/promise](https://github.com/then/promise)
- [https://github.com/reactphp/promise](https://github.com/reactphp/promise)
- [https://github.com/kriskowal/q](https://github.com/kriskowal/q)
- [https://github.com/petkaantonov/bluebird](https://github.com/petkaantonov/bluebird)
- [https://github.com/cujojs/when](https://github.com/cujojs/when)

But obviously, they were all too heavy. In fact, for a library, 80% of people only need 20% of the code. So, I found [https://github.com/stackp/promisejs](https://github.com/stackp/promisejs). Looking at its usage, this was the functionality we needed:

```javascript
function late(n) {
    var p = new promise.Promise();
    setTimeout(function() {
        p.done(null, n);
    }, n);
    return p;
}

late(100).then(
    function(err, n) {
        return late(n + 200);
    }
).then(
    function(err, n) {
        return late(n + 300);
    }
).then(
    function(err, n) {
        return late(n + 400);
    }
).then(
    function(err, n) {
        alert(n);
    }
);
```

Then I opened it to look at the Promise object. It had the features we needed, but also had some features beyond our requirements. Next, I removed the unnecessary features. The function finally became:

```javascript
function Promise() {
    this._callbacks = [];
}

Promise.prototype.then = function(func, context) {
    var p;
    if (this._isdone) {
        p = func.apply(context, this.result);
    } else {
        p = new Promise();
        this._callbacks.push(function () {
            var res = func.apply(context, arguments);
            if (res && typeof res.then === 'function') {
                res.then(p.done, p);
            }
        });
    }
    return p;
};

Promise.prototype.done = function() {
    this.result = arguments;
    this._isdone = true;
    for (var i = 0; i < this._callbacks.length; i++) {
        this._callbacks[i].apply(null, arguments);
    }
    this._callbacks = [];
};

var promise = {
    Promise: Promise
};
```

Note: Pay attention to the `License`. Different software has different licenses, such as MIT, GPL, etc. It's best to use others' code while following their license agreements.

### Implementing the Second Requirement

Since many existing libraries are available, we can directly reference (or copy) code written by others.

```javascript
Lettuce.get = function (url, callback) {
    Lettuce.send(url, 'GET', callback);
};

Lettuce.load = function (url, callback) {
    Lettuce.send(url, 'GET', callback);
};

Lettuce.post = function (url, data, callback) {
    Lettuce.send(url, 'POST', callback, data);
};

Lettuce.send = function (url, method, callback, data) {
    data = data || null;
    var request = new XMLHttpRequest();
    if (callback instanceof Function) {
        request.onreadystatechange = function () {
            if (request.readyState === 4 && (request.status === 200 || request.status === 0)) {
                callback(request.responseText);
            }
        };
    }
    request.open(method, url, true);
    if (data instanceof Object) {
        data = JSON.stringify(data);
        request.setRequestHeader('Content-Type', 'application/json');
    }
    request.setRequestHeader('X-Requested-With', 'XMLHttpRequest');
    request.send(data);
};
```