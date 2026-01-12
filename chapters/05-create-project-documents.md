# Creating Project Documentation

We need to create documentation for our project. Typically, we can refer to everything outside the core code as documentation:

1.  README
2.  Documentation
3.  Examples
4.  Tests

Usually, there's a project introduction at the very top of the project page, as shown in the image below:

![GitHub Project Introduction](../img/github-intro.png)

## README

The README is usually displayed below the GitHub project description, as shown in the image below:

![GitHub README](../img/readme-example.png)

A good README often sparks immediate interest in the project.

For example, here's the introduction from the React project:

![React README](../img/react-intro.png)

The following content clearly states its purposes:

*   **Just the UI:** Lots of people use React as the V in MVC. Since React makes no assumptions about the rest of your technology stack, it's easy to try it out on a small feature in an existing project.
*   **Virtual DOM:** React abstracts away the DOM from you, giving a simpler programming model and better performance. React can also render on the server using Node, and it can power native apps using [React Native](https://facebook.github.io/react-native/).
*   **Data flow:** React implements one-way reactive data flow which reduces boilerplate and is easier to reason about than traditional data binding.

Typically, a README will also include:

*   Target Audience
*   Installation Guide
*   Examples
*   Supported Platforms
*   How to Contribute
*   License

## Official Website and Online Documentation

Many open-source projects have their own websites with documentation. Others host it on platforms like [https://readthedocs.org/](https://readthedocs.org/).

> Read the Docs hosts documentation, making it fully searchable and easier to find. You can import documentation managed with any common version control system, including Mercurial, Git, Subversion, and Bazaar. We support webhooks, so documentation can be automatically built when you commit code. It also supports versioning, allowing you to build documentation from a specific tag or branch in your code repository. See the full feature list.

In an open-source project, good and professional documentation is extremely important. Sometimes it might be even more important than the software itself. Because if an open-source project is useful, most people may not look at the software's code. This means that most of the time, they are interacting with your documentation. Documentation generally includes: API documentation, configuration guides, help files, user manuals, tutorials, etc.

There are many tools for writing documentation, such as Markdown, Doxygen, Docbook, etc.

## Usable Examples

A simple, easy-to-follow example is crucial, especially since we often use an open-source project for a specific purpose and want to integrate it into our project immediately.

What you'd hope to see is opening a browser, entering the code below, and then **It Works**:

```
var HelloMessage = React.createClass({
  render: function() {
    return <div>Hello {this.props.name}</div>;
  }
});

React.render(
  <HelloMessage name="John" />,
  document.getElementById('container')
);
```

Rather than needing complicated steps to proceed.