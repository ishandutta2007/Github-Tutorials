# Introduction

## GitHub

Wikipedia describes it as:

> GitHub is a shared virtual hosting service for storing software code and content projects using Git version control. It was developed by GitHub, Inc. (formerly Logical Awesome) developers Chris Wanstrath, PJ Hyett, and Tom Preston-Werner, written in Ruby on Rails.

Let's also look at the official introduction:

> GitHub is the best place to share code with friends, co-workers, classmates, and complete strangers. Over eight million people use GitHub to build amazing things together.

What else can it be used for?

- A website
- A free blog
- Managing profiles
- Collecting materials
- A resume
- Managing code snippets
- Hosting a programming environment
- Writing

And so on. It seems like a feast, but what else do you need to know?

### Version Management and Software Deployment

When jQuery[^jQuery] released version `2.1.3`, it had 152 commits. We can see commit messages like:

 - Ajax: Always use script injection in globalEval … bbdfbb4
 - Effects: Reintroduce use of requestAnimationFrame … 72119e0
 - Effects: Improve raf logic … 708764f
 - Build: Move test to appropriate module fbdbb6f
 - Build: Update commitplease dev dependency
 - ...

### GitHub and Git

> Git is a distributed version control system originally written by Linus Torvalds for managing Linux kernel development. After its launch, Git achieved great success in other projects, especially within the Ruby community. Currently, many well-known projects including Rubinius, Merb, and Bitcoin use Git. Git can also be used by deployment tools like Capistrano and Vlad the Deployer.

> GitHub can host various Git repositories and provides a web interface. However, unlike other services such as SourceForge or Google Code, GitHub's unique selling point is the ease of forking from another project. Contributing code to a project is very simple: first, click the "fork" button on the project site, check out the code, add your modifications to the forked repository, and finally request a code merge from the project maintainer via the built-in "pull request" mechanism. Some have already called GitHub the MySpace for coders.

[^jQuery]: jQuery is a cross-browser JavaScript library that simplifies interactions between HTML and JavaScript.

## Making the Most of GitHub

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

### Refactoring

I don't want to talk too much about `Refactoring` here. For more details on refactoring, refer to Martin Fowler's book "Refactoring."

What I want to say is: only when the code is covered by tests can we ensure no errors occur during refactoring.
