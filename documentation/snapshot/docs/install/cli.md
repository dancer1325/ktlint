* goal
  * `ktlint`'s CL interface

## Download and verification

### Download manually from github

All releases of `ktlint` can be downloaded from the [releases](https://github.com/pinterest/ktlint/releases) page.

### Download using curl

A particular version of `ktlint` can be downloaded with next command which also changes the file to an executable in directory `/usr/local/bin`:

```sh title="Download"
curl -sSLO https://github.com/pinterest/ktlint/releases/download/1.7.1/ktlint && chmod a+x ktlint && sudo mv ktlint /usr/local/bin/
```

!!! tip "Curl not installed or behind proxy"
    If you don't have curl installed - replace `curl -sL` with `wget -qO-`.  
    If you are behind a proxy see - [curl](https://curl.haxx.se/docs/manpage.html#ENVIRONMENT) / [wget](https://www.gnu.org/software/wget/manual/wget.html#Proxies) manpage. Usually simple:  
    ```shell
    http_proxy=http://proxy-server:port https_proxy=http://proxy-server:port curl -sL ...
    ```

### Verification of download

`ktlint.asc` contains PGP signature which you can verify with:

```sh title="Verify releases 0.32.0 and above"
curl -sS https://keybase.io/ktlint/pgp_keys.asc | gpg --import && gpg --verify ktlint.asc
```

```sh title="Verify releases up through 0.31.0"
curl -sS https://keybase.io/shyiko/pgp_keys.asc | gpg --import && gpg --verify ktlint.asc
```

### Package managers

`ktlint` can be installed via several OS specific package managers.

* brew
  * install 
    * [brew | macOS](https://brew.sh/) OR
    * [Homebrew | Linux](https://docs.brew.sh/Homebrew-on-Linux)
  * `brew install ktlint`

* [MacPorts](https://www.macports.org/)
  * install it
  * `port install ktlint`

## how to use CL?

### Rule set(s)

* [standard ruleset](../rules/standard.md)
  * == rules / 👀apply | ALL CURRENT directory (recursively)'s Kotlin files ('*.kt' OR '*.kts') 👀/
    * ⚠️skip hidden folders⚠️
  * use cases
    * `ktlint`
      * == ❌NO specify arguments❌
      * == default validation / standard ruleset 
  * if you want to run the experimental rules -> set ".editorconfig"'s `ktlint_experimental = enabled`

* if you want to validate with a [custom ruleset](../api/custom-rule-set.md) ->

    ```shell title="Validation with standard + custom ruleset"
    ktlint --ruleset=/path/to/custom-ruleset.jar
    # or
    ktlint -R /path/to/custom-ruleset.jar
    ```
  * if it contains experimental rules & you want to run -> set ".editorconfig"'s `ktlint_experimental = enabled`

### Format (autocorrect)

```shell title="Autocorrect style violations"
ktlint --format
# or
ktlint -F
```

* if 
  * errors are NOT corrected -> printed | `stderr`
  * there are style violations -> AUTOMATICALLY corrected

### Globs

Globs can be used to specify more exactly what files and directories are to be validated. `ktlint` uses the [`.gitignore` pattern style syntax for globs](https://git-scm.com/docs/gitignore). Globs are processed from left to right. Prepend a glob with `!` to negate it. Hidden folders will be skipped.

```shell title="Check only certain locations starting from the current directory"
# Check all '.kt' files in 'src/' directory, but ignore files ending with 'Test.kt':
ktlint 'src/**/*.kt' '!src/**/*Test.kt'

# Check all '.kt' files in 'src/' directory, but ignore 'generated' directory and its subdirectories:
ktlint 'src/**/*.kt' '!src/**/generated/**'
```

### Violation reporting

`ktlint` supports different type of reporters for lint violations. When not specified the `plain` reporter is used. Optionally the `plain` reporter can group the violations per file.

```shell title="Style violation grouped by file"
$ ktlint --reporter=plain?group_by_file
```

When using `ktlint` on an existing project, the number of violations can be huge. To get more insights in which rules are causing the most violations, the `plain-summary` reporter can be used.
```shell title="Style violations counted per rule"
$ ktlint --reporter=plain-summary
```

Other built-in reporters are: `json`, `sarif`, `checkstyle`, and `html`

Style violations can be written to an output file which is convenient when multiple reporters are specified. In example below, the plain reporter is used to write to the console while the checkstyle reports is written to a file:

```shell title="Multiple reporters"
ktlint --reporter=plain --reporter=checkstyle,output=ktlint-report-in-checkstyle-format.xml
```

If resolving all existing errors in a project is unwanted, it is possible to create a baseline and in following invocations compare violations against this baseline. Violations that are registered in the baseline, will be ignored silently. Remove the baseline file in case you want to reset it.

```shell title="Check against a baseline file"
ktlint --baseline=ktlint-baseline.xml # Baseline is created when not existing
```

### Logging

* Logging information
  * 👀written | `stdout`👀
  * `--log-level` OR `-l` /
    * ALLOWED values
      * `trace`
      * `debug`
      * `info`
        * default one
        * == display log lines / 's level == `info`, `warn` OR `error`
      * `warn`
      * `error`
      * `none`

### Rule configuration (".editorconfig")

* [".editorconfig"](../rules/configuration-ktlint.md)
  * allows
    * customizing SOME rules
  * 👀ways to generate a scaffold of the ".editorconfig"👀

    ```shell title="Generate .editorconfig"
    # Specify the code style (ktlint_official, intellij_idea or android_studio) to be used when generating the .editorconfig
    ktlint generateEditorConfig --code-style ktlint_official
    # or
    ktlint --ruleset=/path/to/custom-ruleset.jar generateEditorConfig --code-style android_studio
    ```
  * located
    * 👀NORMALLY, | your project directory's root 👀
      * Reason: 🧠ONLY apply | location's sub folderS🧠
      * ⚠️ALTHOUGH, Ktlint AUTOMATICALLY detects & reads ALL project's ".editorconfig" files⚠️  
  * if you want to specify NON default ".editorconfig" -> 
  
    ```shell title="Override '.editorconfig'"
    ktlint --editorconfig=pathRelativeOrAbsoluteToA.editorconfig
    ```
    * if a property is NOT defined | any ".editorconfig" -> use the value | default ".editorconfig"

### Stdin && stdout

* `ktlint --stdin`
  * the input is read -- from -- `stdin` /
    * you can specify the path -- via -- `stdin-path` 
    
      ```shell title="file path from stdin-path"
      ktlint --stdin --stdin-path /path/to/file/Foo.kt  # /path/to/file/Foo.kt NOT modified -- by -- stdin-path
      ```

  * the violations are printed | `stderr`
  * logging is written | `stdout`

* `ktlint --stdin -F`
  * the violations are printed | `stderr`
  * the formatted code is written | `stdout`

* if you want to suppress 
  * logging (== | `stdout`)
    * by setting `--log-level=none` (see [logging](#logging)) 
  * error output (== | `stderr`)
    * ways
      * ALL error output -> | CL's end, add `2> /dev/null`
      * specify a [reporter](#violation-reporting) / write the error output | file

### Git hooks

Predefined git hooks can be installed, to automatically validate lint errors before commit or push.

```shell title="Install git pre-commit hook"
ktlint installGitPreCommitHook
```

```shell title="Install git pre-push hook"
ktlint installGitPrePushHook
```

### Miscellaneous flags and commands

`--color` and `--color-name=<colorName>`: Make output colorful and optionally set the color name to use.

`-h` or `--help`: Prints help information.

`--limit=<limit>`: Maximum number of errors to show (default: show all)

`--relative`: Print files relative to the working directory (e.g. dir/file.kt instead of /home/user/project/dir/file.kt)

`--patterns-from-stdin[=<delimiter>]`: Reads additional patterns from `stdin`, where the patterns are separated by `<delimiter>`. If `=<delimiter>` is omitted, newline is used as fallback delimiter. If an empty string is given, the `NUL` byte is used as delimiter instead.
If this option is given, then the default patterns are disabled.
Options `--stdin` and `--patterns-from-stdin` are mutually exclusive, only one of them can be given at a time.

`-V` or `--version`: Prints version information and exit.

### Microsoft Windows users

Microsoft Windows is not able to run the `ktlint` command directly. Ktlint can be run in following ways on Microsoft Windows:

1. Use the `ktlint.bat` batch file provided as part of the [release](https://github.com/pinterest/ktlint/releases/tag/1.7.1). Add the batch file to your `%PATH%` environment variable for easy access
2. Run `ktlint` using Git Bash
3. Run as `java -jar ktlint`
