# Recommended setup

* goal
  * recommended setup /
    * maximize your productivity
    * get feedback EARLY -- following -- the failing fast principle

## [ktlint-intellij-plugin](https://plugins.jetbrains.com/plugin/15057-ktlint)

* enable
  * 👀| code, direct feedback👀 /
    * ⚠️per-project setting⚠️ 

* recommendations
  * v0.20.0+

* ALLOWED modes
  * 'distract free'
    * 👀Ktlint formatting is applied AUTOMATICALLY AFTER👀
      * apply Intellij IDEA format, OR
      * save the file
    * ⚠️ONLY display as error the violations / need to be MANUALLY corrected⚠️
    
      ![ktlint-intellij-plugin-distract-free-mode-1.png](..%2Fassets%2Fimages%2Fktlint-intellij-plugin-distract-free-mode-1.png)
      * 👀if you select 'Show all Ktlint violations in file' -> ALL individual violation is shown -- as -- error👀
      
        ![ktlint-intellij-plugin-manual-mode.png](..%2Fassets%2Fimages%2Fktlint-intellij-plugin-manual-mode.png)

    * use cases
      * projects / ".editorconfig" ALREADY set up properly for the project
  * 'manual'
    * 👀if you select 'Show all Ktlint violations in file' -> ALL individual violation is shown -- as -- error👀
            
      ![ktlint-intellij-plugin-manual-mode.png](..%2Fassets%2Fimages%2Fktlint-intellij-plugin-manual-mode.png)
  * disabled entirely

  ![ktlint-intellij-plugin-preferences.png](..%2Fassets%2Fimages%2Fktlint-intellij-plugin-preferences.png)

* if you want to suppress violations / reported by ktlint -> add a `@Suppress` annotation

  ![ktlint-intellij-plugin-suppress-violation.png](..%2Fassets%2Fimages%2Fktlint-intellij-plugin-suppress-violation.png)

## [Git pre-commit hook](cli.md#git-hooks)

* allows
  * avoid committing code / contain lint violations

* ways to generate
  * -- via -- Ktlint CLI
  * find it [here](/ktlint-cli/src/main/kotlin/com/pinterest/ktlint/cli/internal/GitPreCommitHookSubCommand.kt#L23)

## Build pipeline as last defence

* == | build pipeline,
  * run `ktlint-cli`
    * _Example:_ | Maven projects, [ktlint (linting) task](integrations.md#maven-integration) is bound -- to the -- maven `compile` lifecycle 
    * see [integrations](integrations.md)
    * if lint violation is found -> fail the build
