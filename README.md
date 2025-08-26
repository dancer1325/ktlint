<h1 align="center">
<a href="https://pinterest.github.io/ktlint/">
  <img src="https://cloud.githubusercontent.com/assets/370176/26518284/38b680da-4262-11e7-8d27-2b9e849fb55f.png"/>
</a>
</h1>

<p align="center">
<a href="https://kotlinlang.slack.com/messages/CKS3XG0LS"><img src="https://img.shields.io/badge/slack-@kotlinlang/ktlint-yellow.svg?logo=slack" alt="Join the chat at https://kotlinlang.slack.com"/></a>
<a href="https://formulae.brew.sh/formula/ktlint"><img src="https://img.shields.io/homebrew/v/ktlint.svg" alt="HomeBrew"></a>
</p>

<p align="center">

* == 👀Kotlin linter👀
  * 's goal
    * follow [Kotlin coding conventions](https://kotlinlang.org/docs/reference/coding-conventions.html) & [Android Kotlin Style Guide](https://android.github.io/kotlin-guides/style.html) /
      * [MORE strict](https://github.com/pinterest/ktlint/issues/284#issuecomment-425177186)
  * inspired by
    * | JS,
      * [standard/standard](https://github.com/standard/standard)
    * | Go,
      * [gofmt](https://golang.org/cmd/gofmt/)

## Key features

- ❌NO require configuration❌
- Built-in 
  - Rule sets
  - formatter
    - can fix AUTOMATICALLY lint violations
      - OTHERS need to be fixed MANUALLY
  - reporters
    - `plain`
    - `json`
    - `html`
    - `checkstyle`
- [how to create a custom reporter](documentation/snapshot/docs/api/custom-reporter.md)
- [".editorconfig" support](documentation/snapshot/docs/rules/configuration-ktlint.md)
  - contain
    - ".editorconfig" properties
    - IntelliJ IDEA specific properties
    - Ktlint specific properties
- executable jar
  - == released -- as a -- 1! executable jar / include ALL dependencies
- [disable rules](documentation/snapshot/docs/faq.md#how-do-i-enable-or-disable-a-rule)
- enable extension -- via -- [custom rule sets](documentation/snapshot/docs/api/custom-rule-set.md) + reporters

## Quick start

* Step 1: ways to install
  * `brew install ktlint`
  * [OTHER package managers](documentation/release-latest/docs/install/cli.md#package-managers)
  * -- via -- [maven OR gradle plugins](documentation/release-latest/docs/install/integrations.md)

* Step 2: `ktlint --format` OR `ktlint -F`   
  * lint & format(if possible) | CURRENT directory & below's ALL files / ".kt" & ".kts"

## Documentation

* [here](documentation)
