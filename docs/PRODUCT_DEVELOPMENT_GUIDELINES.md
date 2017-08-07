![JavaScript][javascript-logo]

# Product Development Guidelines &middot; [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
> Delivering valuable, high-quality products is challenging, and requires focused attention and clear communication.
Well-defined, evidence-based guidelines are therefore vital for effective collaboration. The following guidelines are based
on years of experience and retrospectives, but that doesn't make them sacred scripture! In the spirit of continous improvement,
always feel free to suggest new guidelines and to challenge existing norms with a pull request.

## Table of contents

- [Git](#git)
    - [Some Git rules](#some-git-rules)
    - [Git workflow](#git-workflow)
    - [Writing good commit messages](#writing-good-commit-messages)
- [Documentation](#documentation)
- [Environments](#environments)
    - [Consistent dev environments](#consistent-dev-environments)
    - [Consistent dependencies](#consistent-dependencies)
- [Dependencies](#dependencies)
- [Testing](#testing)
- [Structure and Naming](#structure-and-naming)
- [Code style](#code-style)
    - [Some code style guidelines](#code-style-check)
    - [Enforcing code style standards](#enforcing-code-style-standards)
- [Logging](#logging)
- [API](#api)
    - [API design](#api-design)
    - [API security](#api-security)
    - [API documentation](#api-documentation)
- [Licensing](#licensing)

<a name="git"></a>
## 1. Git
![Git][git-logo-image]
<a name="some-git-rules"></a>

### 1.1. Some Git rules

There are a set of rules to keep in mind:

#### ![Source code editor][atom-ide-image] Perform work in a topic branch.

  _Why:_
  >Use an isolated topic branch for parallel product development. Topic branches allow you to submit multiple pull requests without confusion. You can iterate without polluting the master branch with potentially unstable, unfinished code. [read more...](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow)


#### ![Git fork][git-fork-image] Branch out from `develop`.

  _Why:_
  >This way, you can make sure that code in master will almost always build without problems, and can be mostly used directly for releases (this might be overkill for some projects).

#### ![Git forbidden][git-no-entry-image] Never push into `develop` or `master` branch. Make a Pull Request.

  _Why:_
  > It notifies team members that they have completed a feature. It also enables easy peer-review of the code and dedicates forum for discussing the proposed feature.

#### ![Git pull request][git-pull-request-image] Submit a Pull Request as soon as possible.

  _Why:_
  > Pull Requests declare work in progress. Frequent pushes to a Pull Request notify your team members about change, and gives them the opportunity to provide feedback more often. Pull Request pushes also trigger automated CI-services, which help you fail fast and assess quality.

#### ![Git compare][git-compare-image] Update your local `develop` branch with an interactive rebase before you ask for Pull Request approvals.

  _Why:_
  > Rebasing will merge in the requested branch (`master` or `develop`) and apply the commits that you have made locally to the top of the history without creating a merge commit (assuming there were no conflicts). Resulting in a nice and clean history. [read more ...](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

#### ![Git compare][git-resolve-image] Resolve rebase conflicts before Pull Request reviews.

_Why:_
> Rebasing will merge in the requested branch (`master` or `develop`) and apply the commits that you have made locally to the top of t

#### ![CI build success][travis-ci-logo-image] Ensure your topic branch's CI-service checks pass before you ask others to review a Pull Request.

 _Why:_
 > You are about to add your code to a stable branch. If your feature-branch tests fail, there is a high chance that your destination branch build will fail too. Additionally you need to apply code style check before making a Pull Request. It aids readability and reduces the chance of formatting fixes being mingled in with actual changes.

#### ![Git pull request review][git-pr-review-image] Add Reviewers and the Label "Status: Review Needed" when your topic branch is ready for review.

  _Why:_
  > When you add a Reviewer, GitHub (or Bitbucket) notifies teammates that your topic branch meets all Acceptance Criteria and is ready to be merged into the main branch. Adding the label "Status: Review Needed" formally declares the status of your topic branch, and helps teams filter through issues.

#### ![Delete branches][delete-image] Delete local and remote topic branches after merging.

  _Why:_
  > It will clutter up your list of branches with dead branches.It insures you only ever merge the branch back into (`master` or `develop`) once. topic branches should only exist while the work is still in progress.

#### ![Ignore extraneous files][git-ignore-image] Use [this](./.gitignore) `.gitignore` file.

  _Why:_
  > It already has a list of system files that should not be sent with your code into a remote repository. In addition, it excludes setting folders and files for most used editors, as well as most common dependency folders.

#### ![Git repo defense][git-repo-protection-image] Protect your `develop` and `master` branches.

  _Why:_
  > It protects your production-ready branches from receiving unexpected and irreversible changes. read more... [Github](https://help.github.com/articles/about-protected-branches/) and [Bitbucket](https://confluence.atlassian.com/bitbucketserver/using-branch-permissions-776639807.html)

<a name="git-workflow"></a>

### 1.2. Git workflow

Because of most of the reasons above, we use [Feature-branch-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow) with [Interactive Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) and some elements of [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows#gitflow-workflow) (naming and having a develop branch). The main steps are as follow:

* For a new project, initialize a git repository in the project directory. __For subsequent features/changes this step should be ignored__.
   ```sh
   cd <project directory>
   git init
   ```

* Checkout a new feature/bug-fix branch.
    ```sh
    git checkout -b <branchname>
    ```
* Make Changes.
    ```sh
    git add
    git commit -a
    ```
    _Why:_
    > `git commit -a` will start an editor which lets you separate the subject from the body. Read more about it in *section 1.3*.

* Sync with remote to get changes you’ve missed.
    ```sh
    git checkout develop
    git pull
    ```

    _Why:_
    > This will give you a chance to deal with conflicts on your machine while rebasing(later) rather than creating a Pull Request that contains conflicts.

* Update your topic branch with latest changes from develop by interactive rebase.
    ```sh
    git checkout <branchname>
    git rebase -i --autosquash develop
    ```

    _Why:_
    > You can use --autosquash to squash all your commits to a single commit. Nobody wants many commits for a single feature in develop branch. [read more...](https://robots.thoughtbot.com/autosquashing-git-commits)

* If you don’t have conflict skip this step. If you have conflicts, [resolve them](https://help.github.com/articles/resolving-a-merge-conflict-using-the-command-line/)  and continue rebase.
    ```sh
    git add <file1> <file2> ...
    git rebase --continue
    ```
* Push your branch. Rebase will change history, so you'll have to use `-f` to force changes into the remote branch. If someone else is working on your branch, use the less destructive `--force-with-lease`.
    ```sh
    git push -f
    ```

    _Why:_
    > When you do a rebase, you are changing the history on your topic branch. As a result, Git will reject normal `git push`. Instead, you'll need to use the -f or --force flag. [read more...](https://developer.atlassian.com/blog/2015/04/force-with-lease/)


* Make a Pull Request.
* Pull request will be accepted, merged and close by a reviewer.
* Remove your local topic branch if you're done.

  ```sh
  git branch -d <branchname>
  ```
  to remove all branches which are no longer on remote
  ```sh
  git fetch -p && for branch in `git branch -vv | grep ': gone]' | awk '{print $1}'`; do git branch -D $branch; done
  ```

<a name="writing-good-commit-messages"></a>
### 1.3 Writing good commit messages

Well-defined commit message guidelines makes working with Git and collaborating with others a lot easier. Enforcing the  with [`commitplease`][commitplease-url] pre-commit hooks

 * Strictly follow the [AngularJS Git Commit Guidelines][git-commit-guidelines-url] (or the [`Conventional Commit Message Specification`][git-commit-guidelines-url] at the very least).

 _Why:_
 > Consistent, legible Git logs not only facilitate communication, but also enable **automated CHANGELOG generation and semantic versioning** with [`standard-version`][standard-version-url].

 * Comply with the Conventional Commit Message format:

 ```text
 <type>(<scope>): <subject>
 <BLANK LINE>
 <body>
 <BLANK LINE>
 <footer>
 ```

 * Begin a commit message with a valid `<type>(<scope>): <subject>`.

 * Separate the subject from the body with a newline between the two.

    _Why:_
    > Git is smart enough to distinguish the first line of your commit message as your summary. In fact, if you try git shortlog, instead of git log, you will see a long list of commit messages, consisting of the id of the commit, and the summary only.

 * Limit the subject line to 50 characters and Wrap the body at 72 characters.

    _why_
    > Commits should be as fine-grained and focused as possible, it is not the place to be verbose. [read more...](https://medium.com/@preslavrachev/what-s-with-the-50-72-rule-8a906f61f09c)

 * Do not end the subject line with a period.
 * Use [imperative mood](https://en.wikipedia.org/wiki/Imperative_mood) in the subject line.

    _Why:_
    > Rather than writing messages that say what a committer has done, it's better to consider these messages as the instructions for what is going to be done after the commit is applied on the repository. [read more...](https://news.ycombinator.com/item?id=2079612)

 * Use the body to explain **what** and **why** as opposed to **how**.
 * Write any associated GitHub (or JIRA) issues in the <footer> to help trace your commits to documented issues and defects.

   _Why:_
   > GitHub (and Bitbucket) automatically hyperlink issue numbers their associated documentation. They also track issue-related commits.

#### 1.3.1. `build` commit messages

Issues related to product builds. The AngularJS Git commit message format is

```
build(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.2. `chore` commit messages

Issues related to miscellaneous non-functional changes (usually "maintenance" changes). The AngularJS Git commit message format is

```
chore(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.3. `ci` commit messages

Issues related to continuous integration, delivery, and deployment tasks. The AngularJS Git commit message format is

```
ci(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.4. `docs` commit messages

Issues related to documentation. The AngularJS Git commit message format is

```
docs(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.5. `feat` (feature) commit messages

New feature or enhancement requests. The AngularJS Git commit message format is

```
feat(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.6. `fix` commit messages

Defect (bug) repair issues. The AngularJS Git commit message format is

```
fix(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.7. `perf` (performance) commit messages

Performance improvement issues. The AngularJS Git commit message format is

```
perf(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.8. `refactor` commit messages

Source code design **improvements that do not affect product behavior**. The AngularJS Git commit message format is

```
refactor(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.9. `revert` commit messages

Tasks that revert to a previous commit hash. Your message should begin with `revert:`, followed by the header of the reverted commit.

In the body it should say: `This reverts commit <hash>.`, where the hash is the SHA of the commit being reverted.

```
revert: <hash>
<BLANK LINE>
This reverts commit <hash>.
<BLANK LINE>
<footer>
```

#### 1.3.10. `style` commit messages

Issues related to style guideline compliance, especially `ESLint` errors and warnings. The AngularJS Git commit message format is

```
style(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

#### 1.3.11. `test` commit messages

Test coverage tasks. The AngularJS Git commit message format is

```
test(<scope>): <subject>
<BLANK LINE>
<[body]>
<BLANK LINE>
<footer>
```

 <a name="documentation"></a>
## 2. Documentation

![Documentation](/.assets/media/img/icons8-documentation.png)

[![ScoreMe README.md grade][readme-score-img]][readme-score-url]

* Use this [template](./README.sample.md) for `README.md`, Feel free to add uncovered sections.
* Prefer a static document site generator (like GitBook or GitHub Pages) to host your documentation with additional features.
* When using static document sites, add RunKit blocks so consumers and contributors can execute code samples immediately.
* For projects with more than one repository, provide links to them in their respective `README.md` files.
* Keep `README.md` updated as a project evolves.
* Comment your code with API documentation generator annotations (e.g., JSDoc 3 or ESDoc). Try to make it as clear as possible what you are intending with each major section.
* If there is an open discussion on github or stackoverflow about the code or approach you're using, include the link in your comment.
* Don't use comments as an excuse for a bad code. Keep your code clean.
* Keep comments relevant as your code evolves.
* Assess your `README.md`'s quality with ScoreMe.


  _Why:_
  > Your repository's `README.md` is your product's home page for consumers and contributors. ScoreMe uses the same calculations as those applied to CocoaPods libraries.

<a name="environments"></a>
## 3. Environments

![Environments](/images/laptop.png)

* Define separate `development`, `test` and `production` environments if needed.

    _Why:_
    > Different data, tokens, APIs, ports etc... might be needed on different environments. You may want an isolated `development` mode that calls fake API which returns predictable data, making both automated and manually testing much easier. Or you may want to enable Google Analytics only on `production` and so on. [read more...](https://stackoverflow.com/questions/8332333/node-js-setting-up-environment-specific-configs-to-be-used-with-everyauth)


* Load your deployment specific configurations from environment variables and never add them to the codebase as constants, [look at this sample](./config.sample.js).

    _Why:_
    > You have tokens, passwords and other valuable information in there. Your config should be correctly separated from the app internals as if the codebase could be made public at any moment.

    _How:_
    >Use `.env` files to store your variables and add them to `.gitignore` to be excluded. Instead, commit a `.env.example`  which serves as a guide for developers. For production, you should still set your environment variables in the standard way.
    [read more](https://medium.com/@rafaelvidaurre/managing-environment-variables-in-node-js-2cb45a55195f)

* It’s recommended to validate environment variables before your app starts.  [Look at this sample](./configWithTest.sample.js) using `joi` to validate provided values.

    _Why:_
    > It may save others from hours of troubleshooting.

<a name="consistent-dev-environments"></a>
### 3.1 Consistent dev environments:
* Set your node version in `engines` in `package.json`.

    _Why:_
    > It lets others know the version of node the project works on. [read more...](https://docs.npmjs.com/files/package.json#engines)

* Additionally, use `nvm` and create a  `.nvmrc`  in your project root. Don't forget to mention it in the documentation.

    _Why:_
    > Any one who uses `nvm` can simply use `nvm use` to switch to the suitable node version. [read more...](https://github.com/creationix/nvm)

* It's a good idea to setup a `preinstall` script that checks node and npm versions.

    _Why:_
    > Some dependencies may fail when installed by newer versions of npm.

* Use Docker image if you can.

    _Why:_
    > It can give you a consistent environment across the entire workflow. Without much need to fiddle with dependencies or configs. [read more...](https://hackernoon.com/how-to-dockerize-a-node-js-application-4fbab45a0c19)

* Use local modules instead of using globally installed modules.

    _Why:_
    > Lets you share your tooling with your colleague instead of expecting them to have it globally on their systems.


<a name="consistent-dependencies"></a>
### 3.2 Consistent dependencies:

* Make sure your team members get the exact same dependencies as you.

    _Why:_
    > Because you want the code to behave as expected and identical in any development machine [read more...](https://medium.com/@kentcdodds/why-semver-ranges-are-literally-the-worst-817cdcb09277)

    _how:_
    > Use `package-lock.json` on `npm@5` or higher

    _I don't have npm@5:_
    > Alternatively you can use `Yarn` and make sure to mention it in `README.md`. Your lock file and `package.json` should have the same versions after each dependency update. [read more...](https://yarnpkg.com/en/)

    _I don't like the name `Yarn`:_
    > Too bad. For older versions of `npm`, use `—save --save-exact` when installing a new dependency and create `npm-shrinkwrap.json` before publishing. [read more...](https://docs.npmjs.com/files/package-locks)

<a name="dependencies"></a>
## 4. Dependencies

![Github](/images/modules.png)
[![Dependency Status][daviddm-image]][daviddm-url] [![devDependencies Status][daviddm-dev-image]][daviddm-dev-url] [![StackShare][stack-share-image]][stack-share-url]


* Keep track of your currently available packages: e.g., `npm ls --depth=0`. [read more...](https://docs.npmjs.com/cli/ls)
* See if any of your packages have become unused or irrelevant: `depcheck`. [read more...](https://www.npmjs.com/package/depcheck)

    _Why:_
    > You may include an unused library in your code and increase the production bundle size. Find unused dependencies and get rid of them.

* Before using a dependency, check its download statistics to see if it is heavily used by the community: `npm-stat`. [read more...](https://npm-stat.com/)

    _Why:_
    > More usage mostly means more contributors, which usually means better maintenance, and all of these result in quickly discovered bugs and quickly developed fixes.

* Before using a dependency, check to see if it has a good, mature version release frequency with a large number of maintainers: e.g., `npm view async`. [read more...](https://docs.npmjs.com/cli/view)

    _Why:_
    > Having loads of contributors won't be as effective if maintainers don't merge fixes and patches quickly enough.

* If a less known dependency is needed, discuss it with the team before using it.
* Always make sure your app works with the latest version of its dependencies without breaking: `npm outdated`. [read more...](https://docs.npmjs.com/cli/outdated)

    _Why:_
    > Dependency updates sometimes contain breaking changes. Always check their release notes when updates show up. Update your dependencies one by one, that makes troubleshooting easier if anything goes wrong. Use a cool tool such as [npm-check-updates](https://github.com/tjunnone/npm-check-updates).

* Check to see if the package has known security vulnerabilities with, e.g., [Snyk](https://snyk.io/test?utm_source=risingstack_blog).



<a name="testing"></a>
## 5. Testing
![Testing](/images/testing.png)
* Have a `test` mode environment if needed.

    _Why:_
    > While sometimes end to end testing in `production` mode might seem enough, there are some exceptions: One example is you may not want to enable analytical information on a 'production' mode and pollute someone's dashboard with test data. The other example is that your API may have rate limits in `production` and blocks your test calls after a certain amount of requests.

* Place your test files next to the tested modules using `*.test.js` or `*.spec.js` naming convention, like `moduleName.spec.js`.

    _Why:_
    > You don't want to dig through a folder structure to find a unit test. [read more...](https://hackernoon.com/structure-your-javascript-code-for-testability-9bc93d9c72dc)


* Put your additional test files into a separate test folder to avoid confusion.

    _Why:_
    > Some test files don't particularly relate to any specific implementation file. You have to put it in a folder that is most likely to be found by other developers: `__test__` folder. This name: `__test__`  is also standard now and gets picked up by most JavaScript testing frameworks.

* Write testable code, avoid side effects, extract side effects, write pure functions

    _Why:_
    > You want to test a business logic as separate units. You have to "minimize the impact of randomness and nondeterministic processes on the reliability of your code". [read more...](https://medium.com/javascript-scene/tdd-the-rite-way-53c9b46f45e3)

    > A pure function is a function that always returns the same output for the same input. Conversely, an impure function is one that may have side effects or depends on conditions from the outside to produce a value. That makes it less predictable. [read more...](https://hackernoon.com/structure-your-javascript-code-for-testability-9bc93d9c72dc)

* Use a static type checker

    _Why:_
    > Sometimes you may need a Static type checker. It brings a certain level of reliability to your code. [read more...](https://medium.freecodecamp.org/why-use-static-types-in-javascript-part-1-8382da1e0adb)


* Run tests locally before making any pull requests to `develop`.

    _Why:_
    > You don't want to be the one who caused production-ready branch build to fail. Run your tests after your `rebase` and before pushing your feature-branch to a remote repository.

* Document your tests including instructions in the relevant section of your `README.md` file.

    _Why:_
    > It's a handy note you leave behind for other developers or DevOps experts or QA or anyone who gets lucky enough to work on your code.

<a name="structure-and-naming"></a>
## 6. Structure and Naming
![Structure and Naming](/images/folder-tree.png)
* Organize your files around product features / pages / components, not roles. Also, place your test files next to their implementation.


    **Bad**

    ```
    .
    ├── controllers
    |   ├── product.js
    |   └── user.js
    ├── models
    |   ├── product.js
    |   └── user.js
    ```

    **Good**

    ```
    .
    ├── product
    |   ├── index.js
    |   ├── product.js
    |   └── product.test.js
    ├── user
    |   ├── index.js
    |   ├── user.js
    |   └── user.test.js
    ```

    _Why:_
    > Instead of a long list of files, you will create small modules that encapsulate one responsibility including its test and so on. It gets much easier to navigate through and things can be found at a glance.

* Put your additional test files to a separate test folder to avoid confusion.

    _Why:_
    > It is a time saver for other developers or DevOps experts in your team.

* Use a `./config` folder and don't make different config files for different environments.

    _Why:_
    >When you break down a config file for different purposes (database, API and so on); putting them in a folder with a very recognizable name such as `config` makes sense. Just remember not to make different config files for different environments. It doesn't scale cleanly, as more deploys of the app are created, new environment names are necessary.
    Values to be used in config files should be provided by environment variables. [read more...](https://medium.com/@fedorHK/no-config-b3f1171eecd5)


* Put your scripts in a `./scripts` folder. This includes `bash` and `node` scripts.

    _Why:_
    >It's very likely you may end up with more than one script, production build, development build, database feeders, database synchronization and so on.


* Place your build output in a `./build` folder. Add `build/` to `.gitignore`.

    _Why:_
    >Name it what you like, `dist` is also cool. But make sure that keep it consistent with your team. What gets in there is most likely generated  (bundled, compiled, transpiled) or moved there. What you can generate, your teammates should be able to generate too, so there is no point committing them into your remote repository. Unless you specifically want to.

* Use `PascalCase' 'camelCase` for filenames and directory names. Use  `PascalCase`  only for Components.

* `CheckBox/index.js` should have the `CheckBox` component, as could `CheckBox.js`, but **not** `CheckBox/CheckBox.js` or `checkbox/CheckBox.js` which are redundant.

* Ideally the directory name should match the name of the default export of `index.js`.

    _Why:_
    > Then you can expect what component or module you will receive by simply just importing its parent folder.   

<a name="code-style"></a>
## 7. Code style

[![JavaScript Style Guide](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

<a name="code-style-check"></a>
### 7.1 Some code style guidelines

* Use stage-2 and higher JavaScript (modern) syntax for new projects. For old project stay consistent with existing syntax unless you intend to modernise the project.

    _Why:_
    > This is all up to you. We use transpilers to use advantages of new syntax. stage-2 is more likely to eventually become part of the spec with only minor revisions.

* Include code style check in your build process.

    _Why:_
    > Breaking your build is one way of enforcing code style to your code. It prevents you from taking it less seriously. Do it for both client and server-side code. [read more...](https://www.robinwieruch.de/react-eslint-webpack-babel/)

* Use [ESLint - Pluggable JavaScript linter](http://eslint.org/) to enforce code style.

    _Why:_
    > We simply prefer `eslint`, you don't have to. It has more rules supported, the ability to configure the rules, and ability to add custom rules.

* We use [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) for JavaScript, [Read more](https://www.gitbook.com/book/duk/airbnb-javascript-guidelines/details). Use the javascript style guide required by the project or your team.

* We use [Flow type style check rules for ESLint](https://github.com/gajus/eslint-plugin-flowtype) when using [FlowType](https://flow.org/).

    _Why:_
    > Flow introduces few syntaxes that also need to follow certain code style and be checked.

* Use `.eslintignore` to exclude file or folders from code style check.

    _Why:_
    > You don't have to pollute your code with `eslint-disable` comments whenever you need to exclude a couple of files from style checking.

* Remove any of your `eslint` disable comments before making a Pull Request.

    _Why:_
    > It's normal to disable style check while working on a code block to focus more on the logic. Just remember to remove those `eslint-disable` comments and follow the rules.

* Depending on the size of the task use  `//TODO:` comments or open a ticket.

    _Why:_
    > So then you can remind yourself and others about a small task (like refactoring a function, or updating a comment). For larger tasks  use `//TODO(#3456)` which is enforced by a lint rule and the number is an open ticket.


* Always comment and keep them relevant as code changes. Remove commented blocks of code.

    _Why:_
    > Your code should be as readable as possible, you should get rid of anything distracting. If you refactored a function, don't just comment out the old one, remove it.

* Avoid irrelevant or funny comments, logs or naming.

    _Why:_
    > While your build process may(should) get rid of them, sometimes your source code may get handed over to another company/client and they may not share the same banter.

* Make your names search-able with meaningful distinctions avoid shortened names. For functions Use long, descriptive names. A function name should be a verb or a verb phrase, and it needs to communicate its intention.

    _Why:_
    > It makes it more natural to read the source code.

* Organize your functions in a file according to the step-down rule. Higher level functions should be on top and lower levels below.

    _Why:_
    > It makes it more natural to read the source code.

<a name="enforcing-code-style-standards"></a>
### 7.2 Enforcing code style standards

* Have your editor notify you about code style errors. Use [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier) and [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier) with your existing ESLint configuration. [read more...](https://github.com/prettier/eslint-config-prettier#installation)

* Consider using Git hooks.

    _Why:_
    > Git hooks greatly increase a developer's productivity. Make changes, commit and push to staging or production environments without the fear of breaking builds. [read more...](http://githooks.com/)

* Use Prettier with a precommit hook.

    _Why:_
    > While `prettier` itself can be very powerful, it's not very productive to run it simply as an npm task alone each time to format code. This is where `lint-staged` (and `husky`) come into play. Read more on configuring `lint-staged` [here](https://github.com/okonet/lint-staged#configuration) and on configuring `husky` [here](https://github.com/typicode/husky).


<a name="logging"></a>
## 8. Logging

![Logging](/images/logging.png)

* Avoid client-side console logs in production

    _Why:_
    > Even though your build process can(should) get rid of them, but make sure your code style check gives your warning about console logs.

* Produce readable production logging. Ideally use logging libraries to be used in production mode (such as [winston](https://github.com/winstonjs/winston) or
[node-bunyan](https://github.com/trentm/node-bunyan)).

    _Why:_
    > It makes your troubleshooting less unpleasant with colorization, timestamps, log to a file in addition to the console or even logging to a file that rotates daily. [read more...](https://blog.risingstack.com/node-js-logging-tutorial/)


<a name="api"></a>
## 9. API
<a name="api-design"></a>

![API](/images/api.png)

### 9.1 API design

_Why:_
> Because we try to enforce development of sanely constructed RESTful interfaces, which team members and clients can consume simply and consistently.  

_Why:_
> Lack of consistency and simplicity can massively increase integration and maintenance costs. Which is why `API design` is included in this document.


* We mostly follow resource-oriented design. It has three main factors: resources, collection, and URLs.
    * A resource has data, gets nested, and there are methods that operate against it.
    * A group of resources is called a collection.
    * URL identifies the online location of resource or collection.

    _Why:_
    > This is a very well-known design to developers (your main API consumers). Apart from readability and ease of use, it allows us to write generic libraries and connectors without even knowing what the API is about.

* use kebab-case for URLs.
* use camelCase for parameters in the query string or resource fields.
* use plural kebab-case for resource names in URLs.

* Always use a plural nouns for naming a url pointing to a collection: `/users`.

    _Why:_
    > Basically, it reads better and keeps URLs consistent. [read more...](https://apigee.com/about/blog/technology/restful-api-design-plural-nouns-and-concrete-names)

* In the source code convert plurals to variables and properties with a List suffix.

    _Why_:
    > Plural is nice in the URL but in the source code, it’s just too subtle and error-prone.

* Always use a singular concept that starts with a collection and ends to an identifier:

    ```
    /students/245743
    /airports/kjfk
    ```
* Avoid URLs like this:
    ```
    GET /blogs/:blogId/posts/:postId/summary
    ```

    _Why:_
    > This is not pointing to a resource but to a property instead. You can pass the property as a parameter to trim your response.

* Keep verbs out of your resource URLs.

    _Why:_
    > Because if you use a verb for each resource operation you soon will have a huge list of URLs and no consistent pattern which makes it difficult for developers to learn. Plus we use verbs for something else.

* Use verbs for non-resources. In this case, your API doesn't return any resources. Instead, you execute an operation and return the result. These **are not** CRUD (create, retrieve, update, and delete) operations:

    ```
    /translate?text=Hallo
    ```

    _Why:_
    > Because for CRUD we use HTTP methods on `resource` or `collection` URLs. The verbs we were talking about are actually `Controllers`. You usually don't develop many of these. [read more...](https://byrondover.github.io/post/restful-api-guidelines/#controller)

* The request body or response type is JSON then please follow `camelCase` for `JSON` property names to maintain the consistency.

    _Why:_
    > This is a JavaScript project guideline, Where Programming language for generating JSON as well as Programming language for parsing JSON are assumed to be JavaScript.

* Even though a resource is a singular concept that is similar to an object instance or database record, you should not use your `table_name` for a resource name and `column_name` resource property.

    _Why:_
    > Because your intention is to expose Resources, not your database schema details.

* Again, only use nouns in your URL when naming your resources and don’t try to explain their functionality.

    _Why:_
    > Only use nouns in your resource URLs, avoid endpoints like `/addNewUser` or `/updateUser` .  Also avoid sending resource operations as a parameter.

* Explain the CRUD functionalities using HTTP methods:

    _How:_
    > `GET`: To retrieve a representation of a resource.

    > `POST`: To create new resources and sub-resources.

    > `PUT`: To update existing resources.

    > `PATCH`: To update existing resources. It only updates the fields that were supplied, leaving the others alone.

    > `DELETE`:	To delete existing resources.


* For nested resources, use the relation between them in the URL. For instance, using `id` to relate an employee to a company.

    _Why:_
    > This is a natural way to make resources explorable.

    _How:_

    > `GET      /schools/2/students	` , should get the list of all students from school 2.

    > `GET      /schools/2/students/31`	, should get the details of student 31, which belongs to school 2.

    > `DELETE   /schools/2/students/31`	, should delete student 31, which belongs to school 2.

    > `PUT      /schools/2/students/31`	, should update info of student 31, Use PUT on resource-URL only, not collection.

    > `POST     /schools` , should create a new school and return the details of the new school created. Use POST on collection-URLs.

* Use a simple ordinal number for a version with a `v` prefix (v1, v2). Move it all the way to the left in the URL so that it has the highest scope:
    ```
    http://api.domain.com/v1/schools/3/students
    ```

    _Why:_
    > When your APIs are public for other third parties, upgrading the APIs with some breaking change would also lead to breaking the existing products or services using your APIs. Using versions in your URL can prevent that from happening. [read more...](https://apigee.com/about/blog/technology/restful-api-design-tips-versioning)



* Response messages must be self-descriptive. A good error message response might look something like this:
    ```json
    {
        "code": 1234,
        "message" : "Something bad happened",
        "description" : "More details"
    }
    ```
    or for validation errors:
    ```json
    {
        "code" : 2314,
        "message" : "Validation Failed",
        "errors" : [
            {
                "code" : 1233,
                "field" : "email",
                "message" : "Invalid email"
            },
            {
                "code" : 1234,
                "field" : "password",
                "message" : "No password provided"
            }
          ]
    }
    ```

    _Why:_
    > developers depend on well-designed errors at the critical times when they are troubleshooting and resolving issues after the applications they've built using your APIs are in the hands of their users.


    _Note: Keep security exception messages as generic as possible. For instance, Instead of saying ‘incorrect password’, you can reply back saying ‘invalid username or password’ so that we don’t unknowingly inform user that username was indeed correct and only the password was incorrect._

* Use only these 8 status codes to send with you response to describe whether **everything worked**,
The **client app did something wrong** or The **API did something wrong**.

    _Which ones:_
    > `200 OK` response represents success for `GET`, `PUT` or `POST` requests.

    > `201 Created` for when new instance is created. Creating a new instance, using `POST` method returns `201` status code.

    > `304 Not Modified` response is to minimize information transfer when the recipient already has cached representations.

    > `400 Bad Request` for when the request was not processed, as the server could not understand what the client is asking for.

    > `401 Unauthorized` for when the request lacks valid credentials and it should re-request with the required credentials.

    > `403 Forbidden` means the server understood the request but refuses to authorize it.

    > `404 Not Found` indicates that the requested resource was not found.

    > `500 Internal Server Error` indicates that the request is valid, but the server could not fulfill it due to some unexpected condition.

    _Why:_
    > Most API providers use a small subset HTTP status codes. For example, the Google GData API uses only 10 status codes, Netflix uses 9, and Digg, only 8. Of course, these responses contain a body with additional information.There are over 70 HTTP status codes. However, most developers don't have all 70 memorized. So if you choose status codes that are not very common you will force application developers away from building their apps and over to wikipedia to figure out what you're trying to tell them. [read more...](https://apigee.com/about/blog/technology/restful-api-design-what-about-errors)


* Provide total numbers of resources in your response.
* Accept `limit` and `offset` parameters.

* The amount of data the resource exposes should also be taken into account. The API consumer doesn't always need the full representation of a resource.Use a fields query parameter that takes a comma separated list of fields to include:
    ```
    GET /student?fields=id,name,age,class
    ```
* Pagination, filtering, and sorting don’t need to be supported from start for all resources. Document those resources that offer filtering and sorting.

<a name="api-security"></a>
### 9.2 API security
These are some basic security best practices:

* Don't use basic authentication unless over a secure connection (HTTPS). Authentication tokens must not be transmitted in the URL: `GET /users/123?token=asdf....`

    _Why:_
    > Because Token, or user ID and password are passed over the network as clear text (it is base64 encoded, but base64 is a reversible encoding), the basic authentication scheme is not secure. [read more...](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)

* Tokens must be transmitted using the Authorization header on every request: `Authorization: Bearer xxxxxx, Extra yyyyy`.

* Authorization Code should be short-lived.

* Reject any non-TLS requests by not responding to any HTTP request to avoid any insecure data exchange. Respond to HTTP requests by `403 Forbidden`.

* Consider using Rate Limiting.

    _Why:_
    > To protect your APIs from bot threats that call your API thousands of times per hour. You should consider implementing rate limit early on.

* Setting HTTP headers appropriately can help to lock down and secure your web application. [read more...](https://github.com/helmetjs/helmet)

* Your API should convert the received data to their canonical form or reject them. Return 400 Bad Request with details about any errors from bad or missing data.

* All the data exchanged with the ReST API must be validated by the API.

* Serialize your JSON.

    _Why:_
    > A key concern with JSON encoders is preventing arbitrary JavaScript remote code execution within the browser... or, if you're using node.js, on the server. It's vital that you use a proper JSON serializer to encode user-supplied data properly to prevent the execution of user-supplied input on the browser.

* Validate the content-type and mostly use `application/*json` (Content-Type header).

    _Why:_
    > For instance, accepting the `application/x-www-form-urlencoded` mime type allows the attacker to create a form and trigger a simple POST request. The server should never assume the Content-Type. A lack of Content-Type header or an unexpected Content-Type header should result in the server rejecting the content with a `4XX` response.


<a name="api-documentation"></a>
### 9.3 API documentation
* Fill the `API Reference` section in [README.md template](./README.sample.md) for API.
* Describe API authentication methods with a code sample.
* Explaining The URL Structure (path only, no root URL) including The request type (Method).

For each endpoint explain:
* URL Params If URL Params exist, specify them in accordance with name mentioned in URL section:

    ```
    Required: id=[integer]
    Optional: photo_id=[alphanumeric]
    ```

* If the request type is POST, provide working examples. URL Params rules apply here too. Separate the section into Optional and Required.

* Success Response, What should be the status code and is there any return data? This is useful when people need to know what their callbacks should expect:

    ```
    Code: 200
    Content: { id : 12 }
    ```

* Error Response, Most endpoints have many ways to fail. From unauthorized access to wrongful parameters etc. All of those should be listed here. It might seem repetitive, but it helps prevent assumptions from being made. For example
    ```json
    {
        "code": 403,
        "message" : "Authentication failed",
        "description" : "Invalid username or password"
    }   
    ```


* Use API design tools, There are lots of open source tools for good documentation such as [API Blueprint](https://apiblueprint.org/) and [Swagger](https://swagger.io/).

<a name="licensing"></a>
## 10. Licensing
![Licensing](/images/licensing.png)

Make sure you use resources that you have the rights to use. If you use libraries, remember to look for MIT, Apache or BSD but if you modify them, then take a look into license details. Copyrighted images and videos may cause legal problems.


---
Sources:
[RisingStack Engineering](https://blog.risingstack.com/),
[Mozilla Developer Network](https://developer.mozilla.org/),
[Heroku Dev Center](https://devcenter.heroku.com),
[Airbnb/javascript](https://github.com/airbnb/javascript),
[Atlassian Git tutorials](https://www.atlassian.com/git/tutorials),
[Apigee](https://apigee.com/about/blog),
[Wishtack](https://blog.wishtack.com)

Icons by [icons8](https://icons8.com/)


[atom-ide-image]: /docs/img/icons8/atom-ide.png
[approval-image]: /docs/img/icons8/approval.png
[cancel-image]: /docs/img/icons8/cancel.png
[delete-image]: /docs/img/icons8/delete.png
[git-commit-image]: /docs/img/icons8/git-commit.png
[git-compare-image]: /docs/img/icons8/git-compare.png
[git-resolve-image]: /docs/img/icons8/git-diff-resolve.png
[git-fork-image]: /docs/img/icons8/git-fork.png
[git-ignore-image]: /docs/img/icons8/git-ignore.png
[git-logo-image]: /docs/img/icons8/git-logo.png
[git-merge-image]: /docs/img/icons8/git-merge.png
[git-merged-image]: /docs/img/icons8/git-merged.png
[git-no-entry-image]: /docs/img/icons8/git-no-entry.png
[git-pull-request-image]: /docs/img/icons8/git-pull-request.png
[git-pr-review-image]: /docs/img/icons8/git-pr-review.png
[git-repo-protection-image]: /docs/img/icons8/git-repo-protection.png
[javascript-logo]: /docs/img/icons8/js-filled.png
[travis-ci-logo-image]: /docs/img/icons8/travis-ci-build-passed.png

[api-docs-url]: https://github.com/gregswindle/generator-apiproxy/docs/API.md
[apigee-edge-js-url]: http://docs.apigee.com/api-services/reference/javascript-object-model
[appveyor-img]: https://ci.appveyor.com/api/projects/status/qcsxteena4etjlfe?svg=true
[appveyor-url]: https://ci.appveyor.com/project/gregswindle/generator-apiproxy
[author-url]: https://github.com/gregswindle
[changelog-url]: https://github.com/gregswindle/generator-apiproxy/blob/master/CHANGELOG.md
[codacy-coverage-image]: https://api.codacy.com/project/badge/Coverage/fa4ade3f68a04b9cad26165a59ceb88e
[codacy-coverage-url]: https://www.codacy.com/app/greg_7/generator-apiproxy?utm_source=github.com&utm_medium=referral&utm_content=gregswindle/generator-apiproxy&utm_campaign=Badge_Coverage
[codacy-img]: https://api.codacy.com/project/badge/Grade/fa4ade3f68a04b9cad26165a59ceb88e
[codacy-url]: https://www.codacy.com/app/greg_7/generator-apiproxy?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=gregswindle/generator-apiproxy&amp;utm_campaign=Badge_Grade
[code-of-conduct-url]: https://github.com/gregswindle/generator-apiproxy/blob/master/.github/CODE_OF_CONDUCT.md
[complexity-report-url]: https://github.com/escomplex/complexity-report
[coveralls-img]: https://coveralls.io/repos/github/gregswindle/generator-apiproxy/badge.svg?branch=master
[coveralls-url]: https://coveralls.io/github/gregswindle/generator-apiproxy?branch=master
[daviddm-dev-image]: https://david-dm.org/gregswindle/generator-apiproxy/dev-status.svg
[daviddm-dev-url]: https://david-dm.org/gregswindle/generator-apiproxy?type=dev
[daviddm-image]: https://david-dm.org/gregswindle/generator-apiproxy.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/gregswindle/generator-apiproxy
[editorconfig-url]: http://editorconfig.org/
[eslint-github-url]: https://github.com/eslint/eslint
[fossa-image]: https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fgregswindle%2Fgenerator-apigee-apiproxy.svg?type=shield
[fossa-url]: https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Fgregswindle%2Fgenerator-apigee-apiproxy?ref=badge_shield
[greenkeeper-img]: https://badges.greenkeeper.io/gregswindle/generator-apiproxy.svg
[greenkeeper-url]: https://greenkeeper.io/
[issues-url]: https://github.com/gregswindle/generator-apiproxy/issues
[jsdoc2md-url]: https://github.com/jsdoc2md/jsdoc-to-markdown
[license-image]: https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=flat
[license-url]: https://github.com/gregswindle/generator-apiproxy/blob/master/LICENSE
[lint-def-url]: https://en.wikipedia.org/wiki/Lint_(software)
[makeapullrequest-image]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat
[makeapullrequest-url]: http://makeapullrequest.com
[npm-image]: https://badge.fury.io/js/generator-apiproxy.svg
[npm-url]: https://npmjs.org/package/generator-apiproxy
[nsp-img]: https://nodesecurity.io/orgs/gregswindle/projects/a3912719-529f-457f-9ff6-53fa70d8f475/badge
[nsp-url]: https://nodesecurity.io/orgs/gregswindle/projects/a3912719-529f-457f-9ff6-53fa70d8f475
[pr-url]: https://github.com/gregswindle/generator-apiproxy/pulls
[readme-score-img]: http://readme-score-api.herokuapp.com/score.svg?url=https://github.com/gregswindle/generator-apiproxy
[readme-score-url]: http://clayallsopp.github.io/readme-score?url=https://github.com/gregswindle/generator-apiproxy
[scoreme-url]: http://clayallsopp.github.io/readme-score/
[sonar-cognitive-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=cognitive_complexity
[sonar-cognitive-url]: https://sonarcloud.io/component_measures/metric/cognitive_complexity/list?id=gregswindle-generator-apiproxy
[sonar-complexity-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=function_complexity
[sonar-complexity-url]: https://sonarcloud.io/component_measures/domain/Complexity?id=gregswindle-generator-apiproxy
[sonar-coverage-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=coverage
[sonar-coverage-url]: https://sonarcloud.io/component_measures/domain/Coverage?id=gregswindle-generator-apiproxy
[sonar-gate-img]: http://sonarcloud.io/api/badges/gate?key=gregswindle-generator-apiproxy
[sonar-gate-url]: http://sonarcloud.io/dashboard/index/gregswindle-generator-apiproxy
[sonar-tech-debt-img]: https://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=sqale_debt_ratio
[sonar-tech-debt-url]: https://sonarcloud.io/component_measures/metric/sqale_index/list?id=gregswindle-generator-apiproxy
[swagger-cli-url]: https://github.com/BigstickCarpet/swagger-cli
[swagger-logo-20-img]: https://github.com/gregswindle/generator-apiproxy/blob/master/.assets/media/img/swagger-logo-20.png
[swagger-markdown-url]: https://github.com/syroegkin/swagger-markdown
[swagger-validity-img]: https://img.shields.io/swagger/valid/2.0/http/api.swindle.net/cordova/v6/contacts/openapi.json.svg
[swagger-validity-url]: http://online.swagger.io/validator/debug?url=http://api.swindle.net/cordova/v6/contacts/openapi.json
[travis-image]: https://travis-ci.org/gregswindle/generator-apiproxy.svg?branch=master
[travis-url]: https://travis-ci.org/gregswindle/generator-apiproxy
[stack-share-image]: https://img.shields.io/badge/tech-stack-0690fa.svg?style=flat
[stack-share-url]: https://stackshare.io/gregswindle/generator-apiproxy
[codecov-image]: https://codecov.io/gh/gregswindle/generator-apiproxy/branch/master/graph/badge.svg
[codecov-url]: https://codecov.io/gh/gregswindle/generator-apiproxy
[coveralls-img]: https://coveralls.io/repos/github/gregswindle/generator-apiproxy/badge.svg
[coveralls-url]: https://coveralls.io/github/gregswindle/generator-apiproxy
[sonar-code-smells-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=code_smells
[sonar-code-smells-url]: https://sonarcloud.io/component_measures/metric/code_smells/list?id=gregswindle-generator-apiproxy
[sonar-cognitive-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=cognitive_complexity
[sonar-cognitive-url]: https://sonarcloud.io/component_measures/metric/cognitive_complexity/list?id=gregswindle-generator-apiproxy
[sonar-complexity-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=function_complexity
[sonar-complexity-url]: https://sonarcloud.io/component_measures/domain/Complexity?id=gregswindle-generator-apiproxy
[sonar-coverage-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=coverage
[sonar-coverage-url]: https://sonarcloud.io/component_measures/domain/Coverage?id=gregswindle-generator-apiproxy
[sonar-duplications-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=duplicated_line_density
[sonar-duplications-url]: https://sonarcloud.io/component_measures/domain/Duplications?id=gregswindle-generator-apiproxy
[sonar-gate-img]: http://sonarcloud.io/api/badges/gate?key=gregswindle-generator-apiproxy
[sonar-gate-url]: http://sonarcloud.io/dashboard/index/gregswindle-generator-apiproxy
[sonar-issues-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=blocker_violations
[sonar-issues-url]: https://sonarcloud.io/component_measures/domain/Issues?id=gregswindle-generator-apiproxy
[sonar-maintainability-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_maintainability_rating
[sonar-maintainability-url]: https://sonarcloud.io/component_measures/domain/Maintainability?id=gregswindle-generator-apiproxy
[sonar-reliability-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_reliability_rating
[sonar-reliability-url]: https://sonarcloud.io/component_measures/domain/Reliability?id=gregswindle-generator-apiproxy
[sonar-security-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=vulnerabilities
[sonar-security-url]: https://sonarcloud.io/component_measures/domain/Security?id=gregswindle-generator-apiproxy
[sonar-tech-debt-img]:  https://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=sqale_debt_ratio
[sonar-tech-debt-url]: https://sonarcloud.io/component_measures/metric/sqale_index/list?id=gregswindle-generator-apiproxy
