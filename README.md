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
  - reporters
    - `plain`
    - `json`
    - `html`
    - `checkstyle`
- ".editorconfig" support
- executable jar
- enable extension -- via -- custom rule sets + reporters

## Quick start

* Step 1: ways to install
  * `brew install ktlint`
  * [OTHER package managers](documentation/release-latest/docs/install/cli.md#package-managers)
  * -- via -- [maven OR gradle plugins](documentation/release-latest/docs/install/integrations.md)

* Step 2: `ktlint --format` OR `ktlint -F`   
  * lint & format(if possible) | CURRENT directory & below's ALL files / ".kt" & ".kts"

## Documentation

* [here](documentation)
