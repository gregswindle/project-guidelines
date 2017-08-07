# Source code quality<br><sup><small>July 23, 2017, 19:27:21 UTC</small></sup>

## Table of contents

<!-- toc -->

- [1. Quality gate and measures](#1-quality-gate-and-measures)
  * [1.1. Complexity](#11-complexity)
  * [1.2. Duplications](#12-duplications)
  * [1.3. Issues](#13-issues)
  * [1.4. Maintainability and reliability](#14-maintainability-and-reliability)
  * [1.5. Security](#15-security)
  * [1.6. Tests](#16-tests)
- [2. Complexity details](#2-complexity-details)
  * [2.1. Overall complexity summary](#21-overall-complexity-summary)
  * [2.2. `generators/app/index.js`](#22-generatorsappindexjs)
  * [2.3. `generators/boilerplate/index.js`](#23-generatorsboilerplateindexjs)
  * [2.4. `generators/docs/index.js`](#24-generatorsdocsindexjs)
  * [2.5. `generators/editorconfig/index.js`](#25-generatorseditorconfigindexjs)
  * [2.6. `generators/eslint/index.js`](#26-generatorseslintindexjs)
  * [2.7. `generators/git/index.js`](#27-generatorsgitindexjs)
  * [2.8. `generators/jsc/index.js`](#28-generatorsjscindexjs)
  * [2.9. `generators/nsp/index.js`](#29-generatorsnspindexjs)
  * [2.10. `generators/readme/index.js`](#210-generatorsreadmeindexjs)
- [3. Package size](#3-package-size)

<!-- tocstop -->

<!-- tocend -->

## 1. Quality gate and measures
[![Quality Gate][sonar-gate-img]][sonar-gate-url] `generator-apiproxy` passes SonarCloud's quality gate.
> 📊 Select the badges below for detailed SonarQube reports. For more details, see the [SonarQube Metric Definitions](http://docs.sonarqube.org/display/SONAR/Metric+Definitions).

### 1.1. Complexity

Complexity measures attempt to calculate how testable and maintainable source code is.

| Type                |  Metric, Description |
|---------------------|----------------------|
| **Complexity**      | [![Cognitive complexity][sonar-cognitive-img]][sonar-cognitive-url]<br>How difficult the control flow of a method is to understand, and therefore to maintain. |
| **Complexity**      | [![function_complexity][function_complexity-image]][function_complexity-url]<br>Complexity by function |

### 1.2. Duplications

> When code with a software vulnerability is copied, the vulnerability may
> continue to exist in the copied code if the developer is not aware of such
> copies.[4] Refactoring duplicate code can improve many software metrics, such
> as lines of code, cyclomatic complexity, and coupling. This may lead to
> shorter compilation times, lower cognitive load, less human error, and fewer
> forgotten or overlooked pieces of code.

| Type                |  Metric, Description |
|---------------------|----------------------|
| **Duplications**    | [![duplicated_lines_density][duplicated_lines_density-image]][duplicated_lines_density-url]<br>Lines duplication percentage |
| **Duplications**    | [![new_duplicated_lines_density][new_duplicated_lines_density-image]][new_duplicated_lines_density-url]<br>New lines duplication percentage |

### 1.3. Issues

> Code smell, also known as bad smell, in computer programming code, refers to
> any symptom in the source code of a program that possibly indicates a deeper
> problem.[1] According to Martin Fowler, "a code smell is a surface indication
> that usually corresponds to a deeper problem in the system".[2] Another way
> to look at smells is with respect to principles and quality:[3] "smells are
> certain structures in the code that indicate violation of fundamental design
> principles and negatively impact design quality".

| Type                |  Metric, Description |
|---------------------|----------------------|
| **Issues**          | [![blocker_violations][blocker_violations-image]][blocker_violations-url]<br>No. of blocker issues |
| **Issues**          | [![critical_violations][critical_violations-image]][critical_violations-url]<br>No. of new critical issues |
| **Issues**          | [![new_blocker_violations][new_blocker_violations-image]][new_blocker_violations-url]<br>No. of blocker issues |
| **Issues**          | [![new_critical_violations][new_critical_violations-image]][new_critical_violations-url]<br>No. of new critical issues |

### 1.4. Maintainability and reliability

> Software is very expensive to maintain.  If you don’t continue to update and
> modify an existing software system or component, it’ll eventually stop working.

| Type                |  Metric, Description |
|---------------------|----------------------|
| **Maintainability** | [![code_smells][code_smells-image]][code_smells-url]<br>No. of code smells |
| **Maintainability** | [![new_code_smells][new_code_smells-image]][new_code_smells-url]<br>No. of new code smells |
| **Maintainability** | [![new_maintainability_rating][new_maintainability_rating-image]][new_maintainability_rating-url]<br>New maintainability rating |
| **Maintainability** | [![new_sqale_debt_ratio][new_sqale_debt_ratio-image]][new_sqale_debt_ratio-url]<br>New technical debt ratio |
| **Maintainability** | [![sqale_debt_ratio][sqale_debt_ratio-image]][sqale_debt_ratio-url]<br>technical debt ratio |
| **Reliability**     | [![new_reliability_rating][new_reliability_rating-image]][new_reliability_rating-url]<br>New reliability rating |
| **Size**            | [![comment_lines_density][comment_lines_density-image]][comment_lines_density-url]<br>Percentage of comments |
| **Size**            | [![lines][lines-image]][lines-url]<br>No. of lines (including comments and empty lines) |
| **Size**            | [![ncloc][ncloc-image]][ncloc-url]<br>No. of lines of code (excluding comments and empty lines) |

### 1.5. Security

> Security measures check for vulnerabilities, i.e., threats, attacks, and
> countermeasures in source code that allow an attacker to
> cause harm to the stakeholders of an application.

| Type                |  Metric, Description |
|---------------------|----------------------|
| **Security**        | [![bugs][bugs-image]][bugs-url]<br>No. of bugs |
| **Security**        | [![new_bugs][new_bugs-image]][new_bugs-url]<br>No. of new bugs |
| **Security**        | [![new_security_rating][new_security_rating-image]][new_security_rating-url]<br>New security rating |
| **Security**        | [![new_vulnerabilities][new_vulnerabilities-image]][new_vulnerabilities-url]<br>No. of new vulnerabilities |
| **Security**        | [![vulnerabilities][vulnerabilities-image]][vulnerabilities-url]<br>No. of vulnerabilities |

### 1.6. Tests

> Verification of individual units of source code, sets of one or more computer
> program modules together with associated control data, usage procedures, and
> operating procedures that are tested to determine whether they are fit for use.

| Type                |  Metric, Description |
|---------------------|----------------------|
| **Tests**           | [![coverage][coverage-image]][coverage-url]<br>Unit test coverage percentage |
| **Tests**           | [![it_coverage][it_coverage-image]][it_coverage-url]<br>IT coverage percentage |
| **Tests**           | [![new_coverage][new_coverage-image]][new_coverage-url]<br>Unit test coverage percentage on new code |
| **Tests**           | [![new_it_coverage][new_it_coverage-image]][new_it_coverage-url]<br>IT coverage percentage on new code |
| **Tests**           | [![new_overall_coverage][new_overall_coverage-image]][new_overall_coverage-url]<br>Overall coverage percentage on new code |
| **Tests**           | [![overall_coverage][overall_coverage-image]][overall_coverage-url]<br>Overall coverage percentage |
| **Tests**           | [![skipped_tests][skipped_tests-image]][skipped_tests-url]<br>No. of ignored tests |
| **Tests**           | [![test_errors][test_errors-image]][test_errors-url]<br>No. of tests that have stopped due to an error |
| **Tests**           | [![test_failures][test_failures-image]][test_failures-url]<br>No. of tests whose assertions have failed |
| **Tests**           | [![test_success_density][test_success_density-image]][test_success_density-url]<br>Percentage of tests that have succeeded |

## 2. Complexity details

### 2.1. Overall complexity summary
> **:white_check_mark: Mean per-function cyclomatic complexity: 1**

> * **Change cost: 11%**
> * **Core size: 0%**
> * **First-order density: 0%**
> * **Mean per-function Halstead effort: 239**
> * **Mean per-function logical LOC: 5**
> * **Mean per-function parameter count: 0**
> * **Mean per-module maintainability index: 129**

### 2.2. `generators/app/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                        | Amount     |
|:-------------------------------|-----------:|
| Cyclomatic complexity density  |  11%       |
| Dependency count               |  6         |
| Logical LOC                    |  9         |
| Maintainability index          |  114       |
| Mean parameter count           |  0         |
| Physical LOC                   |  290       |

### 2.3. `generators/boilerplate/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                       | Amount |
|:------------------------------|-----:|
| Cyclomatic complexity density |  17% |
| Dependency count              | 4    |
| Logical LOC                   |  6   |
| Maintainability index         | 123  |
| Mean parameter count          |  0   |
| Physical LOC                  |  143 |

### 2.4. `generators/docs/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                       | Amount |
|:------------------------------|-----:|
| Cyclomatic complexity density |  20% |
| Dependency count               | 3 |
| Logical LOC                    |  5 |
| Maintainability index          |   127 |
| Mean parameter count           |  0 |
| Physical LOC                   |  126 |

### 2.5. `generators/editorconfig/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                       | Amount |
|:------------------------------|-----:|
| Cyclomatic complexity density |  50% |
| Dependency count               | 1 |
| Logical LOC                    |  2 |
| Maintainability index          |   146 |
| Mean parameter count           |  0 |
| Physical LOC                   |  10 |

### 2.6. `generators/eslint/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                       | Amount |
|:------------------------------|-----:|
| Cyclomatic complexity density |  20% |
| Dependency count               | 4 |
| Logical LOC                    |  5 |
| Maintainability index          |   126 |
| Mean parameter count           |  0 |
| Physical LOC                   |  52 |

### 2.7. `generators/git/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                       | Amount |
|:------------------------------|-----:|
| Cyclomatic complexity density |  33% |
| Dependency count               | 2 |
| Logical LOC                    |  3 |
| Maintainability index          |   137 |
| Mean parameter count           |  0 |
| Physical LOC                   |  67 |

### 2.8. `generators/jsc/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                       | Amount |
|:------------------------------|-----:|
| Cyclomatic complexity density |  20% |
| Dependency count               | 3 |
| Logical LOC                    |  5 |
| Maintainability index          |   127 |
| Mean parameter count           |  0 |
| Physical LOC                   |  61 |

### 2.9. `generators/nsp/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                       | Amount |
|:------------------------------|-----:|
| Cyclomatic complexity density |  33% |
| Dependency count               | 2 |
| Logical LOC                    |  3 |
| Maintainability index          |   137 |
| Mean parameter count           |  0 |
| Physical LOC                   |  16 |

### 2.10. `generators/readme/index.js`

> **:white_check_mark: Cyclomatic complexity: 1**

| Measure                       | Amount |
|:------------------------------|-----:|
| Cyclomatic complexity density |  17% |
| Dependency count               | 4 |
| Logical LOC                    |  6 |
| Maintainability index          |   123 |
| Mean parameter count           |  0 |
| Physical LOC                   |  104 |

## 3. Package size

`npm` module size.

```sh
$ pkgfiles

PATH                                                               SIZE     %   
generators/boilerplate/templates/apiproxy/targets/README.md        0 B      0%  
generators/git/templates/gitattributes                             12 B     0%  
generators/boilerplate/templates/apiproxy/resources/jsc/README.md  77 B     0%  
generators/boilerplate/templates/apiproxy/README.md                81 B     0%  
generators/boilerplate/templates/apiproxy/proxies/README.md        89 B     0%  
generators/boilerplate/templates/apiproxy/policies/README.md       90 B     0%  
generators/editorconfig/templates/editorconfig                     171 B    0%  
generators/boilerplate/templates/openapi/README.md                 220 B    0%  
generators/eslint/templates/eslintignore                           226 B    0%  
generators/editorconfig/index.js                                   275 B    0%  
generators/boilerplate/templates/jest.config.json                  335 B    0%  
generators/boilerplate/templates/.assets/media/img/README.md       352 B    0%  
generators/boilerplate/templates/.assets/media/video/README.md     354 B    0%  
generators/api-proxy-generator.js                                  366 B    0%  
generators/boilerplate/templates/.assets/media/audio/README.md     374 B    0%  
generators/nsp/index.js                                            462 B    0%  
generators/boilerplate/templates/.assets/media/README.md           486 B    0%  
generators/docs/templates/SWAGGER.md                               487 B    0%  
index.js                                                           525 B    0%  
generators/docs/complexity/templates/COMPLEXITY.md                 533 B    0%  
LICENSE                                                            549 B    0%  
generators/eslint/templates/npm-scripts.json                       591 B    0%  
generators/docs/templates/JSCS.md                                  603 B    0%  
generators/jsc/templates/jsc                                       616 B    0%  
NOTICE.md                                                          794 B    0%  
generators/boilerplate/templates/.travis.yml                       899 B    0%  
generators/eslint/index.js                                         1.38 kB  1%  
generators/jsc/index.js                                            1.6 kB   1%  
generators/boilerplate/templates/.assets/README.md                 1.6 kB   1%  
generators/git/index.js                                            1.74 kB  1%  
generators/boilerplate/templates/sonar-project.properties          1.87 kB  1%  
generators/boilerplate/templates/.github/ISSUE_TEMPLATE.md         1.89 kB  1%  
generators/boilerplate/templates/npm-scripts.json                  2.01 kB  1%  
generators/util.js                                                 2.22 kB  1%  
generators/readme/index.js                                         2.47 kB  1%  
generators/docs/complexity/index.js                                2.75 kB  2%  
generators/boilerplate/templates/.github/CODE_OF_CONDUCT.md        3.43 kB  2%  
generators/docs/index.js                                           3.48 kB  2%  
package.json                                                       3.89 kB  2%  
generators/boilerplate/index.js                                    4.2 kB   2%  
CHANGELOG.md                                                       4.41 kB  2%  
generators/boilerplate/templates/.github/PULL_REQUEST_TEMPLATE.md  5.06 kB  3%  
generators/app/index.js                                            7.54 kB  4%  
generators/docs/templates/README.md                                8.32 kB  5%  
generators/readme/templates/README.md                              8.81 kB  5%  
generators/eslint/templates/eslintrc                               11.3 kB  6%  
generators/boilerplate/templates/.github/CONTRIBUTING.md           11.6 kB  6%  
generators/git/templates/gitignore                                 16.3 kB  9%  
README.md                                                          25.3 kB  14%
generators/docs/templates/TERMS_OF_SERVICE.md                      38.7 kB  21%

DIR                                                                SIZE     %   
generators/boilerplate/templates/apiproxy/targets/                 0 B      0%  
generators/boilerplate/templates/apiproxy/resources/jsc/           77 B     0%  
generators/boilerplate/templates/apiproxy/resources/               77 B     0%  
generators/boilerplate/templates/apiproxy/proxies/                 89 B     0%  
generators/boilerplate/templates/apiproxy/policies/                90 B     0%  
generators/editorconfig/templates/                                 171 B    0%  
generators/boilerplate/templates/openapi/                          220 B    0%  
generators/boilerplate/templates/apiproxy/                         337 B    0%  
generators/boilerplate/templates/.assets/media/img/                352 B    0%  
generators/boilerplate/templates/.assets/media/video/              354 B    0%  
generators/boilerplate/templates/.assets/media/audio/              374 B    0%  
generators/editorconfig/                                           446 B    0%  
generators/nsp/                                                    462 B    0%  
generators/docs/complexity/templates/                              533 B    0%  
generators/jsc/templates/                                          616 B    0%  
generators/boilerplate/templates/.assets/media/                    1.57 kB  1%  
generators/jsc/                                                    2.21 kB  1%  
generators/boilerplate/templates/.assets/                          3.17 kB  2%  
generators/docs/complexity/                                        3.28 kB  2%  
generators/app/                                                    7.54 kB  4%  
generators/readme/templates/                                       8.81 kB  5%  
generators/readme/                                                 11.3 kB  6%  
generators/eslint/templates/                                       12.2 kB  7%  
generators/eslint/                                                 13.5 kB  7%  
generators/git/templates/                                          16.3 kB  9%  
generators/git/                                                    18.1 kB  10%
generators/boilerplate/templates/.github/                          22 kB    12%
generators/boilerplate/templates/                                  30.9 kB  17%
generators/boilerplate/                                            35.1 kB  19%
generators/docs/templates/                                         48.2 kB  27%
generators/docs/                                                   54.9 kB  30%
generators/                                                        146 kB   80%
.                                                                  182 kB   100%

PKGFILES SUMMARY
Size on Disk with Dependencies  ~182 MB
Size with Dependencies          ~117 MB
Publishable Size                ~182 kB
Number of Directories           33     
Number of Files                 50
```
---

[Apache-2.0][license-url] © [Greg Swindle][gregswindle-url]



[blocker_violations-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=blocker_violations
[blocker_violations-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[bugs-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=bugs
[bugs-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[code_smells-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=code_smells
[code_smells-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[comment_lines_density-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=comment_lines_density
[comment_lines_density-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[coverage-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=coverage
[coverage-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[critical_violations-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=critical_violations
[critical_violations-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[duplicated_lines_density-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=duplicated_lines_density
[duplicated_lines_density-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[function_complexity-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=function_complexity
[function_complexity-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[gregswindle-url]: https://github.com/gregswindle
[it_coverage-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=it_coverage
[it_coverage-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[license-url]: https://www.apache.org/licenses/LICENSE-2.0
[lines-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=lines
[lines-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[ncloc-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=ncloc
[ncloc-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_blocker_violations-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_blocker_violations
[new_blocker_violations-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_bugs-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_bugs
[new_bugs-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_code_smells-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_code_smells
[new_code_smells-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_coverage-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_coverage
[new_coverage-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_critical_violations-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_critical_violations
[new_critical_violations-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_duplicated_lines_density-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_duplicated_lines_density
[new_duplicated_lines_density-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_it_coverage-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_it_coverage
[new_it_coverage-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_maintainability_rating-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_maintainability_rating
[new_maintainability_rating-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_overall_coverage-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_overall_coverage
[new_overall_coverage-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_reliability_rating-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_reliability_rating
[new_reliability_rating-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_security_rating-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_security_rating
[new_security_rating-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_sqale_debt_ratio-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_sqale_debt_ratio
[new_sqale_debt_ratio-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[new_vulnerabilities-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=new_vulnerabilities
[new_vulnerabilities-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[overall_coverage-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=overall_coverage
[overall_coverage-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[public_documented_api_density-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=public_documented_api_density
[public_documented_api_density-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[skipped_tests-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=skipped_tests
[skipped_tests-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[sonar-code-smells-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=code_smells
[sonar-code-smells-url]: https://sonarcloud.io/component_measures/metric/code_smells/list?id=gregswindle-generator-apiproxy
[sonar-cognitive-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=cognitive_complexity
[sonar-cognitive-img]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=cognitive_complexity
[sonar-cognitive-url]: https://sonarcloud.io/component_measures/metric/cognitive_complexity/list?id=gregswindle-generator-apiproxy
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
[sqale_debt_ratio-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=sqale_debt_ratio
[sqale_debt_ratio-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[test_errors-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=test_errors
[test_errors-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[test_failures-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=test_failures
[test_failures-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[test_success_density-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=test_success_density
[test_success_density-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
[vulnerabilities-image]: http://sonarcloud.io/api/badges/measure?key=gregswindle-generator-apiproxy&metric=vulnerabilities
[vulnerabilities-url]: https://sonarcloud.io/component_measures?id=gregswindle-generator-apiproxy
