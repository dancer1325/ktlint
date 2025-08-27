## Access to the latest `master` snapshot

* if a commit is added | `master` branch  -> snapshot build is AUTOMATICALLY uploaded | [Sonatype's snapshots repository](https://central.sonatype.com/repository/maven-snapshots//com/pinterest/ktlint/)
  * kept 90 days
* steps to check ktlint == `<latest-version>-SNAPSHOT`
  * add the Sonatype snapshot repository location |
    * [Maven](#maven)
    * [Gradle](#gradle)
    * [Kotlin development](#kotlin-development-version-snapshot)

### Maven

```xml
...
<repository>
    <id>sonatype-snapshots</id>
    <url>https://central.sonatype.com/repository/maven-snapshots/</url>
    <snapshots>
        <enabled>true</enabled>
    </snapshots>
    <releases>
        <enabled>false</enabled>
    </releases>
</repository>
...
```

### Gradle

```groovy
repositories {
  maven {
    url "https://central.sonatype.com/repository/maven-snapshots/"
  }
}
```

### Kotlin development version snapshot

Additionally, the project publishes snapshots build against the latest kotlin development version
* To use them, change the version of ktlint to `<latest-version>-kotlin-dev-SNAPSHOT`.
