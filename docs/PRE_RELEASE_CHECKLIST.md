# Pre-release checklist for `generator-apiproxy`
> Before you release `generator-apiproxy`, ensure the following conditions are
> met.

## Table of contents

<!-- toc -->

- [1. Tasks](#1-tasks)
- [2. Resources](#2-resources)

<!-- tocstop -->

<!-- tocend -->

## 1. Tasks
> :memo: Source:  [npm-module-checklist](https://github.com/bahmutov/npm-module-checklist)

- [ ] 1. watch the [egghead.io][egghead] series [How to Write an Open Source JavaScript Library][egghead series];
it is extremely useful for any NPM project (OSS or closed-sourced).

- [ ] 2. All specs (unit tests) pass within the currently accepted coverage thresholds.

- [ ] 3. ESLint passes.

- [ ] 4. Code quality gates pass

- [ ] 5. `npm run release -- --dry-run` produces the complete list of `BREAKING CHANGES`, `features`, or `fixes` to be released.

- [ ] 6. Logging library to show more information during debugging or verbose mode.
[debug][debug], [logdown][logdown]

- [ ] 7. CI buids pass for all target hosts.

- [ ] 8. Neither NSP or ESLint report potential vulnerabilities [snyk][snyk], [NodeSecurity][NodeSecurity]

- [ ] 9. Check module published size and white list only necessary files, tree-shaking, deduping, and pruning where possible [tutorial][module size]

- [ ] 10. Lock the exact versions of the top level dependencies.
Use [save-exact][save-exact] NPM setting and [exact-semver][exact-semver] to enforce it.

- [ ] 11. Greenkeeper is set up for automatic pull requests when newer versions of dependencies appear [greenkeeper.io][greenkeeper]

- [ ] 12. If writing a CLI tool, add a way to check if it is out of date and should be upgraded;
[update-notifier][update-notifier]

- [ ] 13. Validate `package.json` values using [grunt-nice-package][grunt-nice-package]
or [fixpack][fixpack]

- [ ] 14. Installation commands and documentation are available and ready.

- [ ] 15. Documentation have been updated. [xplain][xplain] is my own tool for JS to HTML/Markdown
generation

- [ ] 16. Place most of the public API documentation in README file for simple retrieval.
This allows other developers to find relevant sections right from the command line [manpm][manpm]
or by looking up `npm home package-name`

- [ ] 17. Use a library to output the correct plural forms of words in the user messages [pluralize][pluralize]

## 2. Resources

 * [Publishing NPM  Packages](https://docs.npmjs.com/getting-started/publishing-npm-packages)
 * [Npm Production Checklist](http://jbavari.github.io/blog/2015/10/17/npm-production-checklist/)
 * [Node.js Production Checklist](https://blog.risingstack.com/node-js-production-checklist/)
 * [`npm-module-checklist`](https://github.com/bahmutov/npm-module-checklist): Steps to check when starting, working and publishing a module to NPM


---

2017 © Greg Swindle

[egghead]: https://egghead.io
[egghead series]: https://egghead.io/series/how-to-write-an-open-source-javascript-library

[pick testing framework]: http://glebbahmutov.com/blog/picking-javascript-testing-framework/

[eslint]: http://eslint.org/
[jshint]: http://jshint.com/docs/
[jscs]: http://jscs.info/
[gulp-lint-everything]: https://github.com/bahmutov/gulp-lint-everything

[pre-git]: https://github.com/bahmutov/pre-git
[ghooks]: https://www.npmjs.com/package/ghooks

[Codacy]: https://codacy.com/
[CodeClimate]: https://codeclimate.com/
[BitHound]: https://www.bithound.io/

[commitizen]: https://www.npmjs.com/package/commitizen

[debug]: https://github.com/visionmedia/debug
[logdown]: https://github.com/caiogondim/logdown

[validate-commit-msg]: https://www.npmjs.com/package/validate-commit-msg

[git-issues]: https://www.npmjs.com/package/git-issues

[travis]: https://travis-ci.org/
[circle]: https://circleci.com/

[badges]: http://glebbahmutov.com/blog/tightening-node-project/
[nodeico]: https://nodei.co/
[david-dm]: https://david-dm.org/

[module size]: http://glebbahmutov.com/blog/smaller-published-NPM-modules/

[semantic-release]: https://github.com/semantic-release/semantic-release
[semver]: http://semver.org/
[semver important]: https://medium.com/javascript-scene/software-versions-are-broken-3d2dc0da0783#.h96ppopx3
[broken semver]: https://www.youtube.com/watch?v=tc2UgG5L7WM

[save-exact]: https://docs.npmjs.com/misc/config#save-exact
[exact-semver]: https://github.com/bahmutov/exact-semver

[next-update install]: https://github.com/bahmutov/next-update#install
[greenkeeper]: http://greenkeeper.io/

[update-notifier]: https://github.com/yeoman/update-notifier

[snyk]: https://www.npmjs.com/package/snyk
[NodeSecurity]: https://nodesecurity.io/

[grunt-nice-package]: https://github.com/bahmutov/grunt-nice-package
[fixpack]: https://github.com/henrikjoreteg/fixpack

[atom]: https://github.com/atom/atom/blob/master/CONTRIBUTING.md
[lodash]: https://github.com/lodash/lodash/blob/master/CONTRIBUTING.md
[contributing]: https://github.com/blog/1184-contributing-guidelines

[xplain]: https://github.com/bahmutov/xplain

[manpm]: https://github.com/bahmutov/manpm

[pluralize]: https://github.com/blakeembrey/pluralize
