# Java Build Tools

There are 3 popular tools: *Apache Ant*, *Apache Maven* and *Gradle*

## Apache Ant
* Compile source file to classes
* Running unit tests
* Packaging JAR files
* Creating Javadoc
* A wide range of predifined tasks
* Can extend the build with new tasks written in Java

### Ant shortcommings
* XML verbose
* Comlex build logic leads to long and unmaintainable build scripts
* No guidelines, leads to a build file that looks different every time
* No API let you query information about the model at runtime. (For example how many classes have been compiled etc.)
* Hard without Ivy

## Apache Maven
* Standard directory layout (Convention over configuration**
* Build life cycle (phase)
  * Compiling source code
  * Running unit and integration tests
  * Assembling the artifact (for example a JAR file)
  * Deploying the artifact to a local repository
  * Releasing the artifact to a remote repository
* Dependency management
```xml
<dependencies>
  <dependency>
    <groupId>org.hibernate</groupId>
      <artifactId>hibernate-core</artifactId>
    <version>4.1.7.Final</version>
  </dependency>
<dependencies>
```

### Maven shortcommings
* The default structure can be too restrictive
* Writing Maven extensions is overly cumbersome

## Requitements for a next-gen build tool (Gradle)
* Expressive, declarative, maintainable build language
* Standardized project, but with flexibility
* Easy to use and flexible ways to implement custom logic
* Support more than one project
* Support dependency management
* Scalable and high perf builds

## Gradle
* Gradle is Groovy
* Flexible conventions
* Robust and powerful dependency management (transitive dependencies)
* Scalable builds
* Effortless extendibility
* Integration with other build tools
* Communitydriven and company backed
* Wrapper
* Rich CLI

## Continous delivery
