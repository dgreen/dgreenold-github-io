---
layout: post
title: "Update to Using Maven to Build Executable Jar Files"
date: 2021-07-13 22:26
comments: true
categories: java NetBeans maven
---

This is an update to an [earlier post](/blog/2019/09/15/onward-to-maven/).

At the time of writing, [*Apache NetBeans*][apacheNetBeans] is at version 12.4 and there are severl suppliers of JDKs.  The latest LTS version is JDK 11 and the latest MTS is JDK15.

[Apache Maven][] remains the preferred build automation from for new projects.

One area that is remains unpolished (IMO) is the building of a *jar* file that can be run from the command line.  The menu process "Run &#9654; Clean and Build Main Project" will build a *jar* file but it won't configure the manifest so that

```
java -jar jarfile.jar
```

works even when the JDK (or JRE) is on the command line.

The solution discussed in the earlier post involving the modification of POM (Project Object Model) file is still viable.  It is under the Project Files folder in the Project View in NetBeans.  Load the `pom.xml` file into the NetBeans editor.

Quoting from the [source article][solution]:

> You need to add the following XML snippet to your pom.xml, it can go anywhere inside the `<project>` element, I usually put it after the `<properties>` element:

```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.2.0</version>
                <configuration>
                    <archive>
                        <manifest>
                            <addClasspath>true</addClasspath>
                            <mainClass>MAIN CLASS GOES HERE</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

> Just replace **MAIN CLASS GOES HERE** with your main class (with it's package prefix), rebuild and your JAR is now runnable. If you are unsure what to put here, just copy the Main Class settings from the Run tab in your Netbeans Project Properties.

The version number above has been updated to 3.2.0 matching the latest version of the maven-jar-plugin.

After you do this, you can use "Run &#9654; Clean and Build Main Project" in NetBeans to build the *jar* file.  By changing to the Files view (instead of the Project View), you can see the target directory.

The name of the *jar* file will be dependent on your configuration, your project setup but in my habits project, it was `habits-1.0-SNAPSHOT.jar` which one can run from the terminal with

```bash
java -jar habits-1.0-SNAPSHOT.jar
```

assuming that Java has been set up to run at the command line (or you are using the terminal inside NetBeans.)

**Note** that the target directory is erased as part of the clean process of "Run &#9654; Clean and Build Main Project" so you will need to close anything that has files in that space open before re-running the clean process.

## Maven Shade plugin

In a [baeldung article][more], other solutions for making executable jar files are discussed.  The Maven Shade Plugin allows one to include dependent jar files inside the executable jar although you still need the JDK/JRE installed on the execution machine.

To use this approach, you edit the `pom.xml` as above but include the following instead

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-shade-plugin</artifactId>
    <executions>
        <execution>
            <goals>
                <goal>shade</goal>
            </goals>
            <configuration>
                <shadedArtifactAttached>true</shadedArtifactAttached>
                <transformers>
                    <transformer implementation=
                      "org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>MAIN CLASS GOES HERE</mainClass>
                </transformer>
            </transformers>
        </configuration>
        </execution>
    </executions>
</plugin>
```
and insert the full name with package (but not .class) of the class contains the main method inside the <mainClass> container.

[apacheNetBeans]: https://netbeans.apache.org
[Apache Maven]: https://maven.apache.org
[solution]: https://www.moreofless.co.uk/executable-jar-netbeans-maven-no-main-manifest-attribute/
[more]: https://www.baeldung.com/executable-jar-with-maven