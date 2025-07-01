# Package repo for XercesJ 2.12.2 with XSD 1.1 support

This repository is intended to be a repo that facilitates the use of
Apache XercesJ v2.12.2, with XSD 1.1 support. 

Today, Monday, 30 June 2025, there is no artifact on https://mvnrepository.com/
that packages the XercesJ JAR, along with a declaration of all of its
dependencies. Instead, the [downloads page](Xerces-J-bin.2.12.2-xml-schema-1.1.tar.gz) for Xerces
packages a tgz or zip archive of the required xercesImpl.jar (different from vanilla xercesImpl.jar 2.12.2), 
as well as a set of related dependencies. 

As a result it is impossible to have a simple maven project that declares a
dependency on XercesJ v2.12.2 _with XSD1.1 support_.  Good evidence for this
challenge is on
[Stackoverflow](https://www.google.com/search?q=xsd+1.1+xerces+site%3Astackoverflow.com)
with the list of unanswered questions on this topic.

This repo is basically a repackaging of the downloadable Apache archive, into a format that 
Maven can use directly. You can construct a simple maven project file to get the 
dependencies you need. 

## Using it


You can include this into your maven project in this way:

```xml
<?xml version="1.0"?>
<project xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
         xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
   ...
  <packaging>jar</packaging>
  ...
  <repositories>
    <repository>
      <!-- jitpack is a way to get dependencies from Github repos -->
      <id>jitpack.io</id>
      <url>https://jitpack.io</url>
    </repository>
  </repositories>

  <dependencyManagement>
    <dependencies>
      <dependency>
        <!-- this is the repo -->
        <groupId>com.github.DinoChiesa</groupId>
        <artifactId>xercesj-xsd11-package</artifactId>
        <version>20250630</version>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>

  <dependencies>
    <dependency>
      <groupId>com.github.DinoChiesa.xercesj-xsd11-package</groupId>
      <artifactId>xercesImpl-xsd11</artifactId>
      <version>20250630</version>
      <!--
          <version>2.12.2</version>
      -->
    </dependency>

    <dependency>
      <groupId>com.github.DinoChiesa.xercesj-xsd11-package</groupId>
      <artifactId>xml-apis</artifactId>
      <version>20250630</version>
      <!--
          <version>1.4.02</version>
      -->
    </dependency>

    <dependency>
      <groupId>com.github.DinoChiesa.xercesj-xsd11-package</groupId>
      <artifactId>cup-runtime</artifactId>
      <version>20250630</version>
      <!--
          <version>10k</version>
      -->
    </dependency>

    <dependency>
      <groupId>com.github.DinoChiesa.xercesj-xsd11-package</groupId>
      <artifactId>xpath2-processor</artifactId>
      <version>20250630</version>
      <!--
          <version>1.2.1</version>
      -->
    </dependency>

  </dependencies>

    ...
```

Then just `mvn clean package` as usual.
