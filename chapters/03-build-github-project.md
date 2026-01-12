# Building GitHub Projects

## How to Make Good Use of GitHub

How to effectively use GitHub and practice some aspects of agile software development is quite interesting. We can do many things on it, from testing to CI, to automatic deployment.

### Agile Software Development

Obviously, I'm talking nonsense; this doesn't have much to do with agile software development. But I also don't know what the waterfall model is like. Let me talk about what I know about a project's composition:

 - Kanban-style application management (e.g., Trello, essentially managing software features)
 - CI (Continuous Integration)
 - Test coverage
 - Code quality (code smell)

For a team that isn't remote (like a one-person project), Trello, Jenkins, and Jira are not necessary:

> You exist, deep in my mind.

When you're alone, you just need to clearly know what you want. What we still need is CI and testing to improve code quality.

### Testing

Usually, we look for documentation. If there isn't any, what do you look for? Read the source code, or look at the tests?

```javascript
it("specifying response when you need it", function (done) {
  var doneFn = jasmine.createSpy("success");

  lettuce.get('/some/cool/url', function (result) {
    expect(result).toEqual("awesome response");
    done();
  });

  expect(jasmine.Ajax.requests.mostRecent().url).toBe('/some/cool/url');
  expect(doneFn).not.toHaveBeenCalled();

  jasmine.Ajax.requests.mostRecent().respondWith({
    "status": 200,
    "contentType": 'text/plain',
    "responseText": 'awesome response'
  });
});
```

Code source: [https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

The above test case clearly shows the usage, even if it's written a bit sloppily.

Wait, what is testing for? Let me first explain why I wanted to write tests:

 - I don't want to manually test each feature every time I finish a new one. (Automated testing)
 - I don't want to break existing functionality during refactoring and remain unaware.
 - I hesitate to push code because I'm not confident.

Although I'm not a die-hard TDD fan, the purpose of testing is to ensure functionality works correctly. TDD doesn't necessarily make us write higher-quality code. But sometimes TDD is good; it can help us write simpler logic.

Maybe you already know frameworks like `Selenium`, `Jasmine`, `Cucumber`, etc., and have seen tests similar to:

```
 Ajax
   ✓ specifying response when you need it
   ✓ specifying html when you need it
   ✓ should be post to some where
 Class
   ✓ respects instanceof
   ✓ inherits methods (also super)
   ✓ extend methods
 Effect
   ✓ should be able fadein elements
   ✓ should be able fadeout elements
```

Code source: [https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

Each test seems small, but after completing all of them, we get test coverage:

File | Statements | Branches | Functions | Lines
-----|------------|----------|-----------|------
lettuce.js | 98.58% (209 / 212) | 82.98%(78 / 94) | 100.00% (54 / 54) | 98.58% (209 / 212)

Once local tests pass, we add `Travis-CI` to run our tests.

### CI

Although Node.js isn't exactly a language, since we use Node, here's a simple `.travis.yml` example:

```yml
language: node_js
node_js:
  - "0.10"

notifications:
  email: false

before_install: npm install -g grunt-cli
install: npm install
after_success: CODECLIMATE_REPO_TOKEN=321480822fc37deb0de70a11931b4cb6a2a3cc411680e8f4569936ac8ffbb0ab codeclimate < coverage/lcov.info
```

Code source: [https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

After integrating these into `README.md`, we get the earlier image.

CI is crucial for developers working on the same project from different cities. It means the project code becomes more robust when the added features have test coverage.

### Code Quality

Tools like `jslint` only ensure the code is syntactically correct but can't guarantee you haven't written code with bad smells.

 - Duplicate code
 - Overly long functions
 - etc.

`Code Climate` is a tool integrated with GitHub. We can see not only test coverage but also code quality.

First, look at the Ajax class above:

```javascript
Lettuce.get = function (url, callback) {
  Lettuce.send(url, 'GET', callback);
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

Code source: [https://github.com/phodal/lettuce](https://github.com/phodal/lettuce)

[Code Climate](https://codeclimate.com/github/phodal/lettuce/src/ajax.js) highlights several issues:

 - Missing "use strict" statement. (Line 2)
 - Missing "use strict" statement. (Line 14)
 - 'Lettuce' is not defined. (Line 5)

These are minor issues. Sometimes there might be:

 - Similar code found in two :expression_statement nodes (mass = 86)

This means we can refactor the above code; they are duplicate sections.

## Module Separation and Testing

As mentioned before:

> After nearly half a month of effort—understanding the forked code, refactoring, upgrading versions, adjusting, adding new features, adding tests, adding CI, adding sharing—I finally almost finished.

Today, let's talk about how it was done.

Take my previously created [Lettuce](https://github.com/phodal/lettuce) as an example. It includes:

 - Code quality (Code Climate)
 - CI status (Travis CI)
 - Test coverage (96%)
 - Automated testing (`npm test`)
 - Documentation

According to the [Web Developer Roadmap](https://github.com/phodal/awesome-developer), we still need:

 - Version management
 - Automatic deployment

And so on.

### Code Modularization

In the SkillTree source code, it's roughly divided into three parts:

 - namespace function: as the name suggests
 - Calculator, also known as TalentTree, mainly responsible for parsing, generating URLs, avatars, dependencies, etc.
 - Skill: mainly the tips section.

All of this was in a single JS file. For a library, this is good, but for a project, not so much.

The dependent libraries are:

 - jQuery
 - Knockout

Fortunately, Knockout can be managed with Require.js, so I used `Require.js` for management:

```html
<script type="text/javascript" data-main="app/scripts/main.js" src="app/lib/require.js"></script>
```

The `main.js` configuration is as follows:

```javascript
require.config({
  baseUrl: 'app',
  paths:{
    jquery: 'lib/jquery',
    json: 'lib/json',
    text: 'lib/text'
  }
});

require(['scripts/ko-bindings']);

require(['lib/knockout', 'scripts/TalentTree', 'json!data/web.json'], function(ko, TalentTree, TalentData) {
  'use strict';
  var vm = new TalentTree(TalentData);
  ko.applyBindings(vm);
});
```

The text and JSON plugins are mainly used to handle `web.json`, which uses JSON to manage skills. Thus, different classes went into different JS files.

  .
  |____Book.js
  |____Doc.js
  |____ko-bindings.js
  |____Link.js
  |____main.js
  |____Skill.js
  |____TalentTree.js
  |____Utils.js

Added later recommended reading books, etc. Book and Link both inherit from Doc.

```javascript
define(['scripts/Doc'], function(Doc) {
  'use strict';
  function Book(_e) {
    Doc.apply(this, arguments);
  }
  Book.prototype = new Doc();

  return Book;
});
```

This is what was refactored later. The Doc class is a microcosm of a class in Skillock:

```javascript
define([], function() {
  'use strict';
  var Doc = function (_e) {
    var e = _e || {};
    var self = this;

    self.label = e.label || (e.url || 'Learn more');
    self.url = e.url || 'javascript:void(0)';
  };

  return Doc;
});
```

Or rather, this is what an AMD Class should look like. Considering the implicit binding of `this`, the author used `self = this` to avoid this issue. Finally, the object is returned, and we need to `new` it when calling. Most returns in the code are objects, except in the Utils class, where functions are returned:

```javascript
return {
    getSkillsByHash: getSkillsByHash,
    getSkillById: getSkillById,
    prettyJoin: prettyJoin
};
```

Of course, a function is also an object.

### Automated Testing

I've always been used to Travis CI, so I continued using Travis CI. The `.travis.yml` configuration is as shown:

```yml
language: node_js
node_js:
  - "0.10"

notifications:
  email: false

branches:
  only:
    - gh-pages
```

Using gh-pages is because every time we push code, it can automatically test, deploy, etc., which has a lot of benefits.

Next, we need to add a script in `package.json`:

```javascript
"scripts": {
    "test": "mocha"
  }
```

This way, when we push code, all tests will run automatically. Since mocha's main configuration uses `mocha.opts`, we also need to configure `mocha.opts`:

  --reporter spec
  --ui bdd
  --growl
  --colors
  test/spec

The final `test/spec` specifies the test directory.

### JSLint

> JSLint defines a set of coding conventions stricter than the language defined by ECMA. These coding conventions draw from years of rich coding experience, adhering to a long-standing programming principle: just because you can do something doesn't mean you should. JSLint flags coding practices it deems problematic and also points out obvious errors, thereby encouraging good JavaScript coding habits.

When our JS is written unreasonably, the tests will fail:

  line 5   col 25   A constructor name should start with an uppercase letter.
  line 21  col 62   Strings must use singlequote.

This is a method to drive writing more standardized JS.

### Mocha

> Mocha is an excellent JS testing framework that supports TDD/BDD. Combined with should.js/expect/chai/better-assert, it can easily build test cases in various styles.

The final result looks like this:

    Book,Link
      Book Test
        ✓ should return book label & url
      Link Test
        ✓ should return link label & url

### Test Example

Let's briefly look at the Book test:

```javascript
/* global describe, it */

var requirejs = require("requirejs");
var assert = require("assert");
var should = require("should");
requirejs.config({
  baseUrl: 'app/',
  nodeRequire: require
});

describe('Book,Link', function () {
  var Book, Link;
  before(function (done) {
    requirejs(['scripts/Book'], function (Book_Class) {
      Book = Book_Class;
      done();
    });
  });

  describe('Book Test', function () {
    it('should return book label & url', function () {
      var book_name = 'Head First HTML与CSS';
      var url = 'http://www.phodal.com';
      var books = {
        label: book_name,
        url: url
      };

      var _book = new Book(books);
      _book.label.should.equal(book_name);
      _book.url.should.equal(url);
    });
  });
});
```

Because we use `require.js` to manage dependencies on the browser side, when writing tests in the backend to test, we also need to use it to manage our dependencies. This is why this test is so long. In most cases, a test is similar to this. (Using Jasmine might be a better idea, but I'm used to it.)

```javascript
describe('Book Test', function () {
it('should return book label & url', function () {
  var book_name = 'Head First HTML与CSS';
  var url = 'http://www.phodal.com';
  var books = {
    label: book_name,
    url: url
  };

  var _book = new Book(books);
  _book.label.should.equal(book_name);
  _book.url.should.equal(url);
});
});
```

The final assertion is the core of the test, ensuring the test is useful.

## Code Quality and Refactoring

 - When you've written a lot of code, you may not realize there's a lot of duplication.
 - When you've written a lot of tests, you may not know the coverage percentage.

This becomes a problem, so I happened to see a website called Code Climate.

### Code Climate

> Code Climate consolidates the results from a suite of static analysis tools into a single, real-time report, giving your team the information it needs to identify hotspots, evaluate new approaches, and improve code quality.

Simply put:

- Scores our code
- Finds code smells

So, let's start with an example:

| Rating | Name                             | Complexity | Duplication | Churn | C/M  | Coverage | Smells |
| ------ | -------------------------------- | ---------- | ----------- | ----- | ---- | -------- | ------ |
| A      | lib/coap/coap_request_handler.js | 24         | 0           | 6     | 2.6  | 46.4%    | 0      |
| A      | lib/coap/coap_result_helper.js   | 14         | 0           | 2     | 3.4  | 80.0%    | 0      |
| A      | lib/coap/coap_server.js          | 16         | 0           | 5     | 5.2  | 44.0%    | 0      |
| A      | lib/database/db_factory.js       | 8          | 0           | 3     | 3.8  | 92.3%    | 0      |
| A      | lib/database/iot_db.js           | 7          | 0           | 6     | 1.0  | 58.8%    | 0      |
| A      | lib/database/mongodb_helper.js   | 63         | 0           | 11    | 4.5  | 35.0%    | 0      |
| C      | lib/database/sqlite_helper.js    | 32         | 86          | 10    | 4.5  | 35.0%    | 2      |
| B      | lib/rest/rest_helper.js          | 19         | 62          | 3     | 4.7  | 37.5%    | 2      |
| A      | lib/rest/rest_server.js          | 17         | 0           | 2     | 8.6  | 88.9%    | 0      |

The final result obtained after sharing was:

![Coverage][1]

### Code Smells

So we opened `lib/database/sqlite_helper.js` because it had two smells:

Similar code found in two :expression_statement nodes (mass = 86)

In the code at `lib/database/sqlite_helper.js:58…61 < >`:

```javascript
    SQLiteHelper.prototype.deleteData = function (url, callback) {
        'use strict';
        var sql_command = "DELETE FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
        SQLiteHelper.prototype.basic(sql_command, callback);
```

And `lib/database/sqlite_helper.js:64…67 < >`:

```javascript
SQLiteHelper.prototype.getData = function (url, callback) {
    'use strict';
    var sql_command = "SELECT * FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    SQLiteHelper.prototype.basic(sql_command, callback);
```

But this was duplication from a previous modification...

The original code was like this:

```javascript
SQLiteHelper.prototype.postData = function (block, callback) {
    'use strict';
    var db = new sqlite3.Database(config.db_name);
    var str = this.parseData(config.keys);
    var string = this.parseData(block);

    var sql_command = "insert or replace into " + config.table_name + " (" + str + ") VALUES (" + string + ");";
    db.all(sql_command, function (err) {
        SQLiteHelper.prototype.errorHandler(err);
        db.close();
        callback();
    });
};

SQLiteHelper.prototype.deleteData = function (url, callback) {
    'use strict';
    var db = new sqlite3.Database(config.db_name);
    var sql_command = "DELETE FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    db.all(sql_command, function (err) {
        SQLiteHelper.prototype.errorHandler(err);
        db.close();
        callback();
    });
};

SQLiteHelper.prototype.getData = function (url, callback) {
    'use strict';
    var db = new sqlite3.Database(config.db_name);
    var sql_command = "SELECT * FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    db.all(sql_command, function (err, rows) {
        SQLiteHelper.prototype.errorHandler(err);
        db.close();
        callback(JSON.stringify(rows));
    });
};
```

It also indicated a lot of duplication. The refactored code:

```javascript
SQLiteHelper.prototype.basic = function(sql, db_callback){
    'use strict';
    var db = new sqlite3.Database(config.db_name);
    db.all(sql, function (err, rows) {
        SQLiteHelper.prototype.errorHandler(err);
        db.close();
        db_callback(JSON.stringify(rows));
    });

};

SQLiteHelper.prototype.postData = function (block, callback) {
    'use strict';
    var str = this.parseData(config.keys);
    var string = this.parseData(block);

    var sql_command = "insert or replace into " + config.table_name + " (" + str + ") VALUES (" + string + ");";
    SQLiteHelper.prototype.basic(sql_command, callback);
};

SQLiteHelper.prototype.deleteData = function (url, callback) {
    'use strict';
    var sql_command = "DELETE FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    SQLiteHelper.prototype.basic(sql_command, callback);
};

SQLiteHelper.prototype.getData = function (url, callback) {
    'use strict';
    var sql_command = "SELECT * FROM  " + config.table_name + "  where " + URLHandler.getKeyFromURL(url) + "=" + URLHandler.getValueFromURL(url);
    SQLiteHelper.prototype.basic(sql_command, callback);
};
```
