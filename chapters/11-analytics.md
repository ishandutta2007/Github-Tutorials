# GitHub User Analysis

## Generating Charts

How to analyze user data is an interesting question, especially when we have large amounts of data. Besides `matlab`, we can also use `numpy` + `matplotlib`.

Data can be found here:

[https://github.com/gmszone/ml](https://github.com/gmszone/ml)

Final effect chart:

![2014 01 01](../img/2014-01-01.png)

The JSON file to be parsed is located at `data/2014-01-01-0.json`, size 6.6M. Clearly, we might need a strategy of reading only one line at a time. This explains why tools like sublime open it slowly. Now we only need the creation time from the JSON data.

==, what does this file represent?

**From 00:00 to 01:00 on January 1, 2014, users' operations on GitHub. Here users refer to many... There are 4814 entries of data in total, ranging from commit, create to issues.**

### Data Parsing

```python
import json
for line in open(jsonfile):
    line = f.readline()
```

Then parse the JSON:

```python
import dateutil.parser

lin = json.loads(line)
date = dateutil.parser.parse(lin["created_at"])
```

Here, `dateutil` is used because the fresh data is a string that needs to be converted to `dateutil`, then placed into an array. Finally, we have `parse_data`:

```python
def parse_data(jsonfile):
    f = open(jsonfile, "r")
    dataarray = []
    datacount = 0

    for line in open(jsonfile):
        line = f.readline()
        lin = json.loads(line)
        date = dateutil.parser.parse(lin["created_at"])
        datacount += 1
        dataarray.append(date.minute)

    minuteswithcount = [(x, dataarray.count(x)) for x in set(dataarray)]
    f.close()
    return minuteswithcount
```

The line of code below converts the above into:

```python
minuteswithcount = [(x, dataarray.count(x)) for x in set(dataarray)]
```

Such an array to facilitate parsing:

```python
[(0, 92), (1, 67), (2, 86), (3, 73), (4, 76), (5, 67), (6, 61), (7, 71), (8, 62), (9, 71), (10, 70), (11, 79), (12, 62), (13, 67), (14, 76), (15, 67), (16, 74), (17, 48), (18, 78), (19, 73), (20, 89), (21, 62), (22, 74), (23, 61), (24, 71), (25, 49), (26, 59), (27, 59), (28, 58), (29, 74), (30, 69), (31, 59), (32, 89), (33, 67), (34, 66), (35, 77), (36, 64), (37, 71), (38, 75), (39, 66), (40, 62), (41, 77), (42, 82), (43, 95), (44, 77), (45, 65), (46, 59), (47, 60), (48, 54), (49, 66), (50, 74), (51, 61), (52, 71), (53, 90), (54, 64), (55, 67), (56, 67), (57, 55), (58, 68), (59, 91)]
```

### Matplotlib

Before starting, you need to install `matplotlib`:

```bash
sudo pip install matplotlib
```

Then import this library:

      import matplotlib.pyplot as plt

As with the result above, you only need:

<pre><code class="python">
    plt.figure(figsize=(8,4))
    plt.plot(x, y,label = files)
    plt.legend()
    plt.show()
</code></pre>

Final code can be seen:


```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import json
import dateutil.parser
import numpy as np
import matplotlib.mlab as mlab
import matplotlib.pyplot as plt


def parse_data(jsonfile):
    f = open(jsonfile, "r")
    dataarray = []
    datacount = 0

    for line in open(jsonfile):
        line = f.readline()
        lin = json.loads(line)
        date = dateutil.parser.parse(lin["created_at"])
        datacount += 1
        dataarray.append(date.minute)

    minuteswithcount = [(x, dataarray.count(x)) for x in set(dataarray)]
    f.close()
    return minuteswithcount


def draw_date(files):
    x = []
    y = []
    mwcs = parse_data(files)
    for mwc in mwcs:
        x.append(mwc[0])
        y.append(mwc[1])

    plt.figure(figsize=(8,4))
    plt.plot(x, y,label = files)
    plt.legend()
    plt.show()

draw_date("data/2014-01-01-0.json")
```

## Weekly Analysis

Following the previous article, we can analyze users' weekly submission situations to derive their actual work efficiency. Each programmer's work schedule may be different, such as:

![Phodal Huang's Report](../img/phodal-results.png)

This is my weekly situation. Obviously, if we move Saturday to the front, as work hours increase, GitHub usage declines. As

      a fulltime hacker who works best in the evening (around 8 pm).

However, this is osrc's analysis result.

### Python GitHub Weekly Situation Analysis

Look at an analyzed result:

![Feb Results](../img/feb-results.png)

The result is exactly the opposite of my situation? That seems to be what the graph says, but the data shows this.

    data
    ├── 2014-01-01-0.json
    ├── 2014-02-01-0.json
    ├── 2014-02-02-0.json
    ├── 2014-02-03-0.json
    ├── 2014-02-04-0.json
    ├── 2014-02-05-0.json
    ├── 2014-02-06-0.json
    ├── 2014-02-07-0.json
    ├── 2014-02-08-0.json
    ├── 2014-02-09-0.json
    ├── 2014-02-10-0.json
    ├── 2014-02-11-0.json
    ├── 2014-02-12-0.json
    ├── 2014-02-13-0.json
    ├── 2014-02-14-0.json
    ├── 2014-02-15-0.json
    ├── 2014-02-16-0.json
    ├── 2014-02-17-0.json
    ├── 2014-02-18-0.json
    ├── 2014-02-19-0.json
    └── 2014-02-20-0.json

We captured the situation at 00:00 each night. As for why it's 00:00, I think the data volume might be smaller then. Excluding January 1st, the above is the result. With only one week of data, one might think it's because it was a holiday in China at that time, but it doesn't seem very reliable. Although there are many programmers in China, the number active on GitHub might not be that large, until listing each week's data.

      6570, 7420, 11274, 12073, 12160, 12378, 12897,
      8474, 7984, 12933, 13504, 13763, 13544, 12940,
      7119, 7346, 13412, 14008, 12555

### Python Data Analysis

I rewrote a new method to calculate submission counts. Only later did I realize we could just count lines, but the method is a bit hacky.

```python
def get_minutes_counts_with_id(jsonfile):
    datacount, dataarray = handle_json(jsonfile)
    minuteswithcount = [(x, dataarray.count(x)) for x in set(dataarray)]
    return minuteswithcount


def handle_json(jsonfile):
    f = open(jsonfile, "r")
    dataarray = []
    datacount = 0

    for line in open(jsonfile):
        line = f.readline()
        lin = json.loads(line)
        date = dateutil.parser.parse(lin["created_at"])
        datacount += 1
        dataarray.append(date.minute)

    f.close()
    return datacount, dataarray


def get_minutes_count_num(jsonfile):
    datacount, dataarray = handle_json(jsonfile)
    return datacount


def get_month_total():
    """

    :rtype : object
    """
    monthdaycount = []
    for i in range(1, 20):
        if i < 10:
            filename = 'data/2014-02-0' + i.__str__() + '-0.json'
        else:
            filename = 'data/2014-02-' + i.__str__() + '-0.json'
        monthdaycount.append(get_minutes_count_num(filename))
    return monthdaycount
```

Next, we need to traverse each result. Later on, we'll find this efficiency is really too low; why no multithreading?

### Python Matplotlib Charts

Let our matplotlib do these charting tasks.

```python
if __name__ == '__main__':
    results = pd.get_month_total()
    print results

    plt.figure(figsize=(8, 4))
    plt.plot(results.__getslice__(0, 7), label="first week")
    plt.plot(results.__getslice__(7, 14), label="second week")
    plt.plot(results.__getslice__(14, 21), label="third week")
    plt.legend()
    plt.show()
```

Blue is the first week, green is the second week, red is the third week, resulting in the above chart.

We still need to optimize the method and add multithreading support.

Let's analyze the previous program and then think of ways to optimize. I saw an article online [http://www.huyng.com/posts/python-performance-analysis/](http://www.huyng.com/posts/python-performance-analysis/) talking about analyzing this part.

## Storing to a Database

### SQLite3

We created a database file named `userdata.db`, then created a table with columns: owner, language, eventtype, name, url.

```python
def init_db():
    conn = sqlite3.connect('userdata.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE userinfo (owner text, language text, eventtype text, name text, url text)''')
```

Then we can query the data. Let's start from the result.

```python
def get_count(username):
    count = 0
    userinfo = []
    condition = 'select * from userinfo where owener = \'' + str(username) + '\''
    for zero in c.execute(condition):
        count += 1
        userinfo.append(zero)

    return count, userinfo
```

When I query `gmszone`, which is myself, I get the following result:

```bash
(u'gmszone', u'ForkEvent', u'RESUME', u'TeX', u'https://github.com/gmszone/RESUME')
(u'gmszone', u'WatchEvent', u'iot-dashboard', u'JavaScript', u'https://github.com/gmszone/iot-dashboard')
(u'gmszone', u'PushEvent', u'wechat-wordpress', u'Ruby', u'https://github.com/gmszone/wechat-wordpress')
(u'gmszone', u'WatchEvent', u'iot', u'JavaScript', u'https://github.com/gmszone/iot')
(u'gmszone', u'CreateEvent', u'iot-doc', u'None', u'https://github.com/gmszone/iot-doc')
(u'gmszone', u'CreateEvent', u'iot-doc', u'None', u'https://github.com/gmszone/iot-doc')
(u'gmszone', u'PushEvent', u'iot-doc', u'TeX', u'https://github.com/gmszone/iot-doc')
(u'gmszone', u'PushEvent', u'iot-doc', u'TeX', u'https://github.com/gmszone/iot-doc')
(u'gmszone', u'PushEvent', u'iot-doc', u'TeX', u'https://github.com/gmszone/iot-doc')
109
```

There are 109 events in total, including `Watch`, `Create`, `Push`, `Fork`, and others.
The main projects are `iot`, `RESUME`, `iot-dashboard`, `wechat-wordpress`.
Next are the languages: `Tex`, `Javascript`, `Ruby`, followed by the project URLs.

Notably:

```bash
-rw-r--r--   1 fdhuang staff 905M Apr 12 14:59 userdata.db
```

This database file is **905M**, but the query results are quite satisfactory, at least compared to the original.

Python comes with built-in support for SQLite3, but we still need to install SQLite3:

```bash
brew install sqlite3
```

or

```bash   
sudo port install sqlite3
```

or for Ubuntu:

```bash
sudo apt-get install sqlite3
```

For openSUSE, naturally:

```bash
sudo zypper install sqlite3
```

Although, using yast2 is also good, isn't it?..

### Data Import

Note that this requires Python 2.7, due to issues with gzip's context manager support.

```python
def handle_gzip_file(filename):
    userinfo = []
    with gzip.GzipFile(filename) as f:
        events = [line.decode("utf-8", errors="ignore") for line in f]

        for n, line in enumerate(events):
            try:
                event = json.loads(line)
            except:

                continue

            actor = event["actor"]
            attrs = event.get("actor_attributes", {})
            if actor is None or attrs.get("type") != "User":
                continue

            key = actor.lower()

            repo = event.get("repository", {})
            info = str(repo.get("owner")), str(repo.get("language")), str(event["type"]), str(repo.get("name")), str(
                repo.get("url"))
            userinfo.append(info)

    return userinfo

def build_db_with_gzip():
    init_db()
    conn = sqlite3.connect('userdata.db')
    c = conn.cursor()

    year = 2014
    month = 3

    for day in range(1,31):
        date_re = re.compile(r"([0-9]{4})-([0-9]{2})-([0-9]{2})-([0-9]+)\.json.gz")

        fn_template = os.path.join("march",
                                   "{year}-{month:02d}-{day:02d}-{n}.json.gz")
        kwargs = {"year": year, "month": month, "day": day, "n": "*"}
        filenames = glob.glob(fn_template.format(**kwargs))

        for filename in filenames:
            c.executemany('INSERT INTO userinfo VALUES (?,?,?,?,?)', handle_gzip_file(filename))

    conn.commit()
    c.close()
```

`executemany` can insert multiple data entries. For our data, an hourly file has about five or six thousand entries that meet our conditions above (i.e., have `actor` and `type`). We only need to record events for users, not all events.

We need to traverse the files and find the appropriate parts. Here, we are only looking for all events from `2014-03-01` to `2014-03-31`. The gzipped files for just this data amount to 1.26G. Decompressing them into JSON files seems inappropriate; we can only process them by traversal.

Here, I referenced the writing style from the osrc project, or rather copied it directly.

First, the regex match:

```python
date_re = re.compile(r"([0-9]{4})-([0-9]{2})-([0-9]{2})-([0-9]+)\.json.gz")
```

But the main part is `glob.glob`:

> glob is a file operation related module that comes with Python. You can use it to find files that match your purpose, similar to file search in Windows, supporting wildcard operations.

Here, `gzip.GzipFile` is also used, another nice thing.

Final code can be seen at:

[github.com/gmszone/ml](http://github.com/gmszone/ml)

A better solution?

### Redis

Query the total number of user events:

```python
import redis
r = redis.StrictRedis(host='localhost', port=6379, db=0)
pipe = pipe = r.pipeline()
pipe.zscore('osrc:user',"gmszone")
pipe.execute()
```

The system returned `227.0`. Let's try someone else.

```bash
>>> pipe.zscore('osrc:user',"dfm")
<redis.client.StrictPipeline object at 0x104fa7f50>
>>> pipe.execute()
[425.0]
>>>
```

See which day had the most submissions:

```python
>>> pipe.hgetall('osrc:user:gmszone:day')
<redis.client.StrictPipeline object at 0x104fa7f50>
>>> pipe.execute()
[{'1': '51', '0': '41', '3': '17', '2': '34', '5': '28', '4': '22', '6': '34'}]
```

The result roughly looks like this:

![SMTWTFS](../img/smtwtfs.png)

See what the main events are?

    >>> pipe.zrevrange("osrc:user:gmszone:event".format("gmszone"), 0, -1,withscores=True)
    <redis.client.StrictPipeline object at 0x104fa7f50>
    >>> pipe.execute()
    [[('PushEvent', 154.0), ('CreateEvent', 41.0), ('WatchEvent', 18.0), ('GollumEvent', 8.0), ('MemberEvent', 3.0), ('ForkEvent', 2.0), ('ReleaseEvent', 1.0)]]

![Main Event](../img/main-events.png)

Blue is push events, yellow is create, etc.

Here, we have understood how the database part of OSRC works.

#### Redis Queries

The main code is as follows:

```python
def get_vector(user, pipe=None):

    r = redis.StrictRedis(host='localhost', port=6379, db=0)
    no_pipe = False
    if pipe is None:
        pipe = pipe = r.pipeline()
        no_pipe = True

    user = user.lower()
    pipe.zscore(get_format("user"), user)
    pipe.hgetall(get_format("user:{0}:day".format(user)))
    pipe.zrevrange(get_format("user:{0}:event".format(user)), 0, -1,
                   withscores=True)
    pipe.zcard(get_format("user:{0}:contribution".format(user)))
    pipe.zcard(get_format("user:{0}:connection".format(user)))
    pipe.zcard(get_format("user:{0}:repo".format(user)))
    pipe.zcard(get_format("user:{0}:lang".format(user)))
    pipe.zrevrange(get_format("user:{0}:lang".format(user)), 0, -1,
                   withscores=True)

    if no_pipe:
        return pipe.execute()
```

The result was displayed in the previous article, which is:

```
[227.0, {'1': '51', '0': '41', '3': '17', '2': '34', '5': '28', '4': '22', '6': '34'}, [('PushEvent', 154.0), ('CreateEvent', 41.0), ('WatchEvent', 18.0), ('GollumEvent', 8.0), ('MemberEvent', 3.0), ('ForkEvent', 2.0), ('ReleaseEvent', 1.0)], 0, 0, 0, 11, [('CSS', 74.0), ('JavaScript', 60.0), ('Ruby', 12.0), ('TeX', 6.0), ('Python', 6.0), ('Java', 5.0), ('C++', 5.0), ('Assembly', 5.0), ('C', 3.0), ('Emacs Lisp', 2.0), ('Arduino', 2.0)]]
```

Interestingly, it generated users similar to me:

```
['alesdokshanin', 'hjiawei', 'andrewreedy', 'christj6', '1995eaton']
```

The most interesting part of osrc is arguably flann, of course, also referring to a very key and interesting part of the system backend design.

## Nearest Neighbor Algorithm and Similar Users

The nearest neighbor algorithm is a very interesting thing in this analysis process.

> The nearest neighbor algorithm, or K-Nearest Neighbor (kNN) classification algorithm, can be said to be the simplest method among all data mining classification techniques. The so-called K-Nearest Neighbor means k nearest neighbors. It says each sample can be represented by its k nearest neighbors.

In other words, we need some samples as our analysis data. Here, what we used is from our previous data.

```
[227.0, {'1': '51', '0': '41', '3': '17', '2': '34', '5': '28', '4': '22', '6': '34'}, [('PushEvent', 154.0), ('CreateEvent', 41.0), ('WatchEvent', 18.0), ('GollumEvent', 8.0), ('MemberEvent', 3.0), ('ForkEvent', 2.0), ('ReleaseEvent', 1.0)], 0, 0, 0, 11, [('CSS', 74.0), ('JavaScript', 60.0), ('Ruby', 12.0), ('TeX', 6.0), ('Python', 6.0), ('Java', 5.0), ('C++', 5.0), ('Assembly', 5.0), ('C', 3.0), ('Emacs Lisp', 2.0), ('Arduino', 2.0)]]
```

In the code, a points.h5 file is constructed to analyze each user's points, which are then recorded in an hdf5 file.

```
[ 0.00438596  0.18061674  0.2246696   0.14977974  0.07488987  0.0969163
    0.12334802  0.14977974  0.          0.18061674  0.          0.          0.
    0.00881057  0.          0.          0.03524229  0.          0.
    0.01321586  0.          0.          0.          0.6784141   0.
    0.07929515  0.00440529  1.          1.          1.          0.08333333
    0.26431718  0.02202643  0.05286344  0.02643172  0.          0.01321586
    0.02202643  0.          0.          0.          0.          0.          0.
    0.          0.          0.00881057  0.          0.          0.          0.
    0.          0.          0.          0.          0.          0.          0.
    0.          0.          0.          0.          0.00881057]
```

This analyzes most of the user's behaviors and then finds users with similar behaviors. The main behaviors include the following:

 - Weekly situation
 - Event types
 - Number of contributions, connections, and languages
 - Top languages

Code used for parsing in osrc:

```python
def parse_vector(results):
    points = np.zeros(nvector)
    total = int(results[0])

    points[0] = 1.0 / (total + 1)

    # Week means.
    for k, v in results[1].iteritems():
        points[1 + int(k)] = float(v) / total

    # Event types.
    n = 8
    for k, v in results[2]:
        points[n + evttypes.index(k)] = float(v) / total

    # Number of contributions, connections and languages.
    n += nevts
    points[n] = 1.0 / (float(results[3]) + 1)
    points[n + 1] = 1.0 / (float(results[4]) + 1)
    points[n + 2] = 1.0 / (float(results[5]) + 1)
    points[n + 3] = 1.0 / (float(results[6]) + 1)

    # Top languages.
    n += 4
    for k, v in results[7]:
        if k in langs:
            points[n + langs.index(k)] = float(v) / total
        else:
            # Unknown language.
            points[-1] = float(v) / total

    return points
```

This returns the points we need. Then we can use `get_points` to get these:

```python
def get_points(usernames):
    r = redis.StrictRedis(host='localhost', port=6379, db=0)
    pipe = r.pipeline()

    results = get_vector(usernames)
    points = np.zeros([len(usernames), nvector])
    points = parse_vector(results)
    return points
```

We will get our corresponding data. Then let's find the ones nearest to me and see the result.

```
[ 0.01298701  0.19736842  0.          0.30263158  0.21052632  0.19736842
    0.          0.09210526  0.          0.22368421  0.01315789  0.          0.
    0.          0.          0.          0.01315789  0.          0.
    0.01315789  0.          0.          0.          0.73684211  0.          0.
    0.          1.          1.          1.          0.2         0.42105263
    0.09210526  0.          0.          0.          0.          0.23684211
    0.          0.          0.03947368  0.          0.          0.          0.
    0.          0.          0.          0.          0.          0.          0.
    0.          0.          0.          0.          0.          0.          0.
    0.          0.          0.          0.        ]
```

I really can't see any similarity between the two...