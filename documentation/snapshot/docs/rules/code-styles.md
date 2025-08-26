* | v1.0,
  * `ktlint_official`
    * == 👀[Kotlin Coding conventions](https://kotlinlang.org/docs/coding-conventions.html) + [Android's Kotlin styleguide](https://developer.android.com/kotlin/style-guide) + ADDITIONAL formatting👀
      * use cases
        * | MOST cases,
          * NICELY formatted code 
        * | SOME cases,
          * ❌code formatting is NOT accepted -- by the -- default code formatters❌
    * == 👀default code style👀
      * if you want to use ANOTHER code style -> set

        ```.editorconfig
        [*.{kt,kts}]
        ktlint_code_style = intellij_idea # or android_studio or ktlint_official (default)
        ```

* `intellij_idea`
  * FORMERLY, `official`
  * == code style /
    * 's goal
      * based -- on -- [Kotlin Coding conventions](https://kotlinlang.org/docs/coding-conventions.html) 
      * 👀compatible -- with -- IntelliJ IDEA's default formatter👀

* `android_studio`
  * FORMERLY, `android`
  * == code style / 
    * 's goal
      * based -- on -- [Android's Kotlin styleguide](https://developer.android.com/kotlin/style-guide) 
      * compatible -- with -- default formatter of Android Studio
