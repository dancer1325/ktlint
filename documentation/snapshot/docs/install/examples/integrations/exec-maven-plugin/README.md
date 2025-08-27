## how has it been created?
* | "integrations/" path
  ```shell
  mvn archetype:generate \
    -DgroupId=com.install.examples.integrations \
    -DartifactId=exec-maven-plugin \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
  ```
* refactor
  * "App.java" -> "Main.kt"
  * "java" folder -> "kotlin" folder
  * remove "AppTest.java"
* | "pom.xml",
  * adjust
    * `<properties>`
    * `<dependencies>`
    * `<build>`
### how to configure ktlint?
* | "pom.xml",
  ```xml
  <plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>3.5.0</version>
    <executions>
      <execution>
        <!--
        Format and autocorrect lint errors when possible during compile. This helps in committing autocorrect changes in the
        same commit as where the original code changes were made.
        -->
        <id>ktlint-format</id>
        <phase>compile</phase>        <!-- == executed | `mvn compile` -->
        <goals>
          <goal>exec</goal>
        </goals>
      </execution>
    </executions>
    <configuration>
      <includePluginDependencies>true</includePluginDependencies>
      <executable>java</executable>
      <arguments>
        <argument>-classpath</argument>           <!-- TODO: check if it's valid -->
        <!-- automatically creates the classpath using all project dependencies, also adding the project build directory -->
        <classpath/>
        <argument>com.pinterest.ktlint.Main</argument>
        <!-- Actual wanted arguments to run ktlint with formatting -->
        <argument>--format</argument>
        <argument>--relative</argument>
      </arguments>
    </configuration>
    <dependencies>
      <dependency>
        <groupId>com.pinterest.ktlint</groupId>
        <artifactId>ktlint-cli</artifactId>
        <version>1.7.1</version>
        <!-- Use fat jar of ktlint-cli -->
        <classifier>all</classifier>
        <type>jar</type>
      </dependency>
      <!-- additional 3rd party ruleset(s) can be specified here -->
    </dependencies>
  </plugin>
  ```


## how to run ktlint?
* `mvn compile` OR `mvn exec:exec@ktlint-format`
