# Maven Notes

- [Maven Notes](#maven-notes)
  - [Introduction](#introduction)
  - [Minimun req for a POM](#minimun-req-for-a-pom)
    - [What is a Plugin?](#what-is-a-plugin)
  - [Important terms](#important-terms)

## Introduction

Apache Maven is a software project management and comprehension tool that provides developers a complete build lifecycle framework. Based on the concept of a [project object model (POM)](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html#:~:text=A%20Project%20Object%20Model%20or,default%20values%20for%20most%20projects). A Project Object Model or POM is a XML file that contains information about the project and configuration details used by Maven to build the project. It contains default values for most projects. Examples for this is the build directory, which is target. When executing a task or goal, Maven looks for the POM in the current directory. It reads the POM, gets the needed configuration information, then executes the goal. 

- The Super POM is Maven's default POM. All POMs extend the Super POM unless explicitly set. [Super POM for maven 3.6.3](https://maven.apache.org/ref/3.6.3/maven-model-builder/super-pom.html)

## Minimun req for a POM

- *project* root
- *modelVersion* - should be set to 4.0.0
- *groupId* - the id of the project's group.
- *artifactId* - the id of the artifact (project)
- *version* - the version of the artifact under the specified group

### What is a Plugin?

## Important terms

- *declarativer programming*  A declarative format is one in which you declare the intention/end-result of the program, instead of how it should be arrived at. ... This is considered a declarative format because the statements convey high-level meaning without specifying low-level actions.
