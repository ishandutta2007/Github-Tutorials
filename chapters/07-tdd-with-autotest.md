# Improving GitHub Project Code Quality: Testing

## TDD

Although I've been exposed to TDD for a while, I've rarely truly practiced it. Apart from teaching others TDD, there were occasional switch sessions during pair programming, perhaps limited by the current development process.

By chance, while developing an IoT-related open-source project—[Lan](https://github.com/phodal/lan)—I revisited this process. It's worth mentioning that in our development process, **tests are written by the developers responsible for the related features**. Sometimes writing tests is quite challenging. Over time, writing tests for my own open-source projects became second nature. Sometimes, not having tests made me feel **insecure**.

### A Test-Driven Development Experience

Previously, I was rewriting a server for [IoT](http://www.phodal.com/iot), mainly combining CoAP, MQTT, HTTP, and other protocols to form an IoT cloud service. The current main task focused on protocols and authorization. Since authorization differs between protocols, I initially wrote an HTTP PUT authorization feature. How was it tested at the very beginning?

    curl --user root:root -X PUT -d '{ "dream": 1 }' -H "Content-Type: application/json" http://localhost:8899/topics/test

As long as I could check for the presence of `req.headers.authorization` in the request, I could proceed, followed by adding a condition. After all, we are quite familiar with the HTTP protocol.

```javascript
if (!req.headers.authorization) {
  res.statusCode = 401;
  res.setHeader('WWW-Authenticate', 'Basic realm="Secure Area"');
  return res.end('Unauthorized');
}
```

But besides HTTP, there are also MQTT and CoAP protocols. For MQTT, it's okay since it has built-in authorization, for example:

```bash
mosquitto_pub -u root -P root -h localhost -d -t lettuce -m "Hello, MQTT. This is my first message."
```

This allows us to simply implement this feature. However, some protocols don't have such functionality; for example, CoAP uses Option for authorization. Current tools like libcoap only have simple functionalities like:

```bash
coap-client -m get coap://127.0.0.1:5683/topics/zero -T
```

So, I first wrote a test script to verify the functionality.

```javascript
var coap     = require('coap');
var request  = coap.request;
var req = request({hostname: 'localhost',port:5683,pathname: '',method: 'POST'});

...

req.setHeader("Accept", "application/json");
req.setOption('Block2',  [new Buffer('phodal'), new Buffer('phodal')]);

...

req.end();
```

After writing the test script, I realized something was off—shouldn't this be test code? So I moved it to the spec directory. Then I wondered, why not implement the entire above functionality using TDD?

### Talking About TDD

Test-Driven Development is a very "ancient" software development methodology. However, due to domestic development processes—where developers are responsible for feature testing—such a good technique hasn't gained traction in China.

The main process of Test-Driven Development is:

1.  Write functional tests first.
2.  Implement the feature code.
3.  Commit the code (commit -> ensuring functionality works).
4.  Refactor the feature code.

For such an IoT project, I already had several advantageous premises:

1.  Already had a prototype.
2.  Framework design.

### TDD Reflection

Usually, in my understanding, TDD is optional. Since I already know most of the features I need to implement, and I also know how to implement them. At the same time, I remain vigilant about Code Smell and ensure features are covered by tests. So overall, TDD doesn't bring much added value.

However, in the current situation, I know what features I want, but I don't understand their deeper functionalities. I need to spend a lot of time understanding why they are the way they are, and I need some scripts to know how they work. TDD becomes very valuable. In other words, in the existing situation, TDD can drive more development for things we don't fully understand. After all, once we complete the test scripts, we also find that these test scripts become part of the code.

Under such ideal circumstances, why wouldn't we use TDD?

## Functional Testing

### Lightweight Website Testing with TWill

> twill was initially designed for testing Web sites, although since then people have also figured out that it's good for browsing unsuspecting Web sites.

The reason it's called lightweight is that it uses command-line testing, has a DSL, and is based on Python.

Besides, it can also be used for load testing, but a different kind. It can simulate entire processes, such as how many people are logging into your website simultaneously.

However, it has one limitation: no JavaScript.

Looking at the source code, the basic principle is using `requests` to download HTML, then parsing HTML with `lxml`. What's interesting is it embeds a `DSL`.

This is a Python library.

     pip install twill

### Twill Login Test

1. Start our application.

2. Enter the twill shell

    twill-sh
     -= Welcome to twill! =-
    current page:  *empty page*

3. Open the webpage

    >> go http://127.0.0.1:5000/login
    ==> at http://127.0.0.1:5000/login
    current page: http://127.0.0.1:5000/login

4. Display forms

    	>> showforms

	Form #1
	## ## __Name__________________ __Type___ __ID________ __Value__________________
	1     csrf_token               hidden    csrf_token   1423387196##5005bdf3496e09b8e2fbf450 ...
	2     email                    email     email        None
	3     password                 password  password     None
	4     login                    submit    (None)       登入

	current page: http://127.0.0.1:5000/login

5. Fill the form

    formclear 1
    fv 1 email test@tes.com
    fv 1 password test

6. Modify the action

    formaction 1 http://127.0.0.1:5000/login

7. Submit the form

    >> submit
    Note: submit is using submit button: name="login", value="登入"
    current page: http://127.0.0.1:5000/

We found it redirected to the homepage.

### Twill Test Script

Of course, we can also use a script directly to test: `login.twill`:

	go http://127.0.0.1:5000/login

	showforms
	formclear 1
	fv 1 email test@tes.com
	fv 1 password test
	formaction 1 http://127.0.0.1:5000/login
	submit

	go http://127.0.0.1:5000/logout

Run

     twill-sh login.twill

Result

	>> EXECUTING FILE login.twill
	AT LINE: login.twill:0
	==> at http://127.0.0.1:5000/login
	AT LINE: login.twill:2

	Form #1
	## ## __Name__________________ __Type___ __ID________ __Value__________________
	1     csrf_token               hidden    csrf_token   1423387345##7a000b612fef39aceab5ca54 ...
	2     email                    email     email        None
	3     password                 password  password     None
	4     login                    submit    (None)       登入

	AT LINE: login.twill:3
	AT LINE: login.twill:4
	AT LINE: login.twill:5
	AT LINE: login.twill:6
	Setting action for form  (<Element form at 0x10e7cbb50>,) to  ('http://127.0.0.1:5000/login',)
	AT LINE: login.twill:7
	Note: submit is using submit button: name="login", value="登入"

	AT LINE: login.twill:9
	==> at http://127.0.0.1:5000/login
	--
	1 of 1 files SUCCEEDED.

A successful test was born.

## Fake Server

I practiced how to fake a server using sinon, haven't used respondWith yet, so let's write about it.

Here, we need to use the sinon framework for testing.

When we do a fetch, we can return our desired fake result.

        var data = {"id":1,"name":"Rice","type":"Good","price":12,"quantity":1,"description":"Made in China"};
	beforeEach(function() {
		this.server = sinon.fakeServer.create();
		this.rices = new Rices();
		this.server.respondWith(
			"GET",
			"http://localhost:8080/all/rice",
			[
				200,
				{"Content-Type": "application/json"},
				JSON.stringify(data)
			]
		);
	});

So in afterEach, we need to restore this server.

	afterEach(function() {
		this.server.restore();
	});

Then write a jasmine test to test it.

	describe("Collection Test", function() {
		it("should get data from the url", function() {
			this.rices.fetch();
			this.server.respond();
			var result = JSON.parse(JSON.stringify(this.rices.models[0]));
			expect(result["id"])
				.toEqual(1);
			expect(result["price"])
				.toEqual(12);
			expect(result)
				.toEqual(data);
		});
	});