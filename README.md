[![Logo of the project][product-logo-image]](README.md)

# Name of the project

Display a list of badges&mdash;preferably in this order&mdash;so that consumers and contributors can easily scan the current and historical status of your product.

`<license-badge>`, `<license-scan-results-badge>`, `<product-semantic-version-badge>`
<br>`<security-vulnerabilities-badge>`, `<product-dependencies-badge>`, `<product-development-dependencies-badge>`
<br>`<build-status-badge>`, `<code-coverage-badge>`, `<code-quality-badge>`

> Additional information or tag line.

A brief description of your project, what it is used for.

## Table of contents

Install [`markdown-toc`][markdown-toc-url] and automate its execution to keep a current table of contents with jump-links.

<!-- toc -->

- [Installation / Getting started](#installation--getting-started)
- [Usage](#usage)
- [Development](#development)
  * [Built With](#built-with)
  * [Prerequisites](#prerequisites)
  * [Set up a development environment](#set-up-a-development-environment)
- [DevSecOps](#devsecops)
  * [Build](#build)
  * [Test](#test)
  * [Deploy/Publish](#deploypublish)
- [Version and Change Log](#version-and-change-log)
- [Configuration](#configuration)
- [Style guide](#style-guide)
- [API Reference](#api-reference)
- [Datastore(s)](#datastores)
- [Contributions](#contributions)
  * [Contributor recognition](#contributor-recognition)
- [License](#license)
  * [`product-name's` license](#product-names-license)
  * [Third-party dependencies' licenses](#third-party-dependencies-licenses)

<!-- tocstop -->

<!-- tocend -->

## Installation / Getting started

A quick introduction of the minimal setup you need to get a hello world up &
running.

```shell
$ npm install <product-name>
```

If your team prefers Yarn:

```sh
$ yarn add <product-name>
```

Here you should say what actually happens when you execute the code above.

## Usage

Once installed, describe your product's features and how to use them. __For large products, consider publishing to a static site like GitHub Pages or GitBook.__

## Development

Provide a link to your [product development guidelines][product-development-guidelines-url].

### Built With

List main libraries, frameworks used including versions (React, Angular etc.). Automate this list dynamically in order to keep it up-to-date.

### Prerequisites

What is needed to set up the dev environment. For instance, global dependencies or any other tools. Provide installation instructions using dependency management tools. (If dependency management is not available, include download links.)

### Set up a development environment

Here's a brief intro about what a developer must do in order to start developing
the project further:

```shell
git clone https://github.com/your/your-project.git
cd your-project/
packagemanager install
```

And state what happens step-by-step. If there is any virtual environment, local server or database feeder needed, explain here.

## DevSecOps

Briefly state the continuous integration/continuous delivery (or deployment) services you use for product delivery, including all quantity gates.

### Build

If your project needs some additional steps for the developer to build the
project after some code changes, state them here. for example:

```shell
./configure
make
make install
```

Here again you should state what actually happens when the code above gets
executed.

### Test

Describe and show how to run the tests with code examples.
Explain what these tests test and why.

```shell
Give an example
```

### Deploy/Publish

Give instructions on how to build and release a new version.
In case there's some step you have to take that publishes this project to a
server, this is the right time to state it.

```shell
packagemanager deploy your-project -s server.com -u username -p password
```

And again you'd need to tell what the previous code actually does.

## Version and Change Log

Use [SemVer](http://semver.org/) for versioning, and declare the latest version here. For the versions available, see the [link to tags on this repository](/tags).

Finally, link to the Change Log, which describes that features, fixes, and breaking changes introduced over time, with links to their Git commits SHAs.

The latest version of `<product-name>` is `1.0.1`. View the [CHANGELOG][changelog-url] for details.


## Configuration

Here you should write what are all of the configurations a user can enter when
using the project.

## Style guide

Explain your code style and show how validate and fix non-compliant source code with `ESLint`.

## API Reference

If your product depends on external APIs, link to the API documentation.

If your product **is an API or micro-service**, link to its OpenAPI specification.

## Datastore(s)

Explain what database (and version) has been used. Provide download links.
Documents your database design and schemas, relations etc...

## Contributions

![Alt text](https://camo.githubusercontent.com/f96261621753dacf526590825b84f87ccb1db0e6/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5052732d77656c636f6d652d627269676874677265656e2e7376673f7374796c653d666c6174 "Pull Request") We welcome contributors and pull requests!

Contributions are community-driven stories with a beginning, a middle, and an end, all told through issues, comments, and pull requests. If you're interested in collaborating, please review these guidelines:

* [Code of Conduct][code-of-conduct-url]
* [Contributing][contributing-url] to `<product-name>`
* [Contributor License Agreement][cla-url]
* [Product development guidelines][product-development-guidelines-url]

### Contributor recognition

Contributing to an open source product can be intimidating, and requires our most precious resource: time. Use a tool like [`all-contributors-cli`][all-contributors-cli-url] to automatically generate a table of contributors by name and contribution.

Contributions come in many forms, including:

| Emoji | Type of contribution |
|:-----:|------------|
| 💬 | Answering Questions (in Issues, Stack Overflow, Gitter, Slack, etc.) |
| 🐛 | Bug reports |
| 📝 | Blogposts |
| 💻 | Code |
| 📖 | Documentation |
| 🎨 | Design |
| 💡 | Examples |
| 📋 | Event Organizers |
| 💵 | Financial Support |
| 🔍 | Funding/Grant Finders |
| 🤔 | Ideas & Planning |
| 🚇 | Infrastructure (Hosting, Build-Tools, etc) |
| 🔌 | Plugin/utility libraries |
| 👀 | Reviewed Pull Requests
| 🔧 | Tools |
| 🌍 | Translation |
| ⚠️ | Tests |
| ✅ | Tutorials |
| 📢 | Talks |
| 📹 | Videos |

This demonstrates your gratitude and commitment to community growth.

## License

### `product-name's` license

State what the license is and how to find the text version of the license.

[MIT][license-url] © [Product Owner](https://githbub.com/product-owner)

### Third-party dependencies' licenses

Display the results of your last scan for third-party dependencies included in your product, e.g., from FOSSA.

![FOSSA Status][fossa-image-large]

[all-contributors-cli-url]: https://github.com/kentcdodds/all-contributors
[changelog-url]: ./CHANGELOG.md
[cla-url]: https://www.clahub.com/agreements/gregswindle/open-api-archetypes
[code-of-conduct-url]: ./CODE_OF_CONDUCT.md
[contributing-url]: ./CONTRIBUTING.md
[fossa-image-large]: https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Forganization%2Frepo-name.svg?type=large
[license-url]: ./LICENSE
[markdown-toc-url]: https://github.com/jonschlinkert/markdown-toc
[product-development-guidelines-url]: /docs/product-development-guidelines/js/PRODUCT_DEVELOPEMENT_GUIDELINES.md
[product-logo-image]: /docs/img/logo.sample.png
