---
layout: post
title: "Onward to Maven in Apache NetBeans"
date: 2019-09-15 11:23
comments: true
categories: java NetBeans CoolBeans maven
---

> An update to this article is [available](/blog/2021/07/13/update-to-using-maven-to-build-executable-jar-files/)

At the time of writing, [*Apache NetBeans*][apacheNetBeans] is at version 11.1 and about 90% moved from Oracle to Apache.   As a project of the Apache Foundation, all source code must be licensed under the [Apache Foundation License][license].  Of course, not all open source is licensed that way (and it was not the open source license used by Oracle) so there are some challenges to putting together large systems.  The [CoolBeans project][CoolBeans] packages NetBeans, the JDK, OpenJavaFx and other components to create an integrated product that is easier to get up and running with.  I will use NetBeans as the tool in the remainder of the post.

Another change made was changing the underlying preferred build automation from [Apache Ant][] to [Apache Maven][] for new projects.  This changes the file structure of the code as well as some details underneath.  NetBeans mostly allows the user to ignore this once the project is made.

One area that is not yet polished (IMO) is the building of a *jar* file that can be run from the command line.  The menu process "Run &#9654; Clean and Build Main Project" will build a *jar* file but it won't configure the manifest so that

```
java -jar jarfile.jar
```

works.

The [solution was posted by Steve Claridge][solution] is to modify the POM (Project Object Model) file.  It is under the Project Files folder in the Project View in NetBeans.  Load the `pom.xml` file into the NetBeans editor.

Quoting from the article:

> You need to add the following XML snippet to your pom.xml, it can go anywhere inside the <project> element, I usually put it after the <properties> element:

```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>2.4</version>
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

After you do this, you can use "Run &#9654; Clean and Build Main Project" in NetBeans to build the *jar* file.  By changing to the Files view (instead of the Project View), you can see the target directory.

The name of the *jar* file will be dependent on your configuration, your project setup but in my habits project, it was `habits-1.0-SNAPSHOT.jar` which one can run from the terminal with

```bash
java -jar habits-1.0-SNAPSHOT.jar
```

assuming that Java has been set up to run at the command line (or you are using the terminal inside NetBeans.)

**Note** that the target directory is erased as part of the clean process of "Run &#9654; Clean and Build Main Project" so you will need to close anything that has files in that space open before re-running the clean process.

[apacheNetBeans]: https://netbeans.apache.org
[license]: http://www.apache.org/licenses/LICENSE-2.0
[CoolBeans]: https://coolbeans.xyz
[Apache Ant]: https://ant.apache.org
[Apache Maven]: https://maven.apache.org
[solution]: https://www.moreofless.co.uk/executable-jar-netbeans-maven-no-main-manifest-attribute/