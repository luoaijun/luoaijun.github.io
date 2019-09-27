
##  How to publish JAR packages to Maven Central Warehouse?


#### 1. Create your maven project 
- [create project](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)
- or you can use idea to create a maven project.

#### 2. Register JIRA account

- **URL**:[https://issues.sonatype.org/secure/Signup!default.jspa](https://issues.sonatype.org/secure/Signup!default.jspa)


---
> You need to fill in Email, Full Name, Username and password, where the next steps of Username and Password need to be used. Please write them down.


#### 3. Create issue 

- **URL**:[https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134)

---
> By creating issues on JIRA to apply for new jar packages, Sonatype staff will review them.

![issue](resources/images/2.png? "create your issue")

#### 4. Create and push your gpg autograph

- ![create and push you gpg autograph](chapter3/chapter3.md)

#### 5. Configure Maven's setting.xml

> the username and password is your JIRA's username and password.
```
<servers>
    <server>
        <id>ossrh</id>
        <username>username</username>
        <password>passsword</password>
    </server>
</servers>
```


#### 6. Configure your project's pom file
> Configure POM information according to Sonatype OSSRH requirements

1. Supply Javadoc and Sources
2. Sign Files with GPG/PGP
3. Sufficient Metadata

```
    - Correct Coordinates
    - Project Name, Description and URL
    - License Information
    - Developer Information
    - SCM Information
```
- This is my pom file ,you can refer to it.
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.luoaijun</groupId>
    <artifactId>utils</artifactId>
    <version>1.0</version>

    <name>luoaijun</name>
    <description>Framework for Advanced Statistics and Data Sciences</description>
    <url>https://github.com/luoaijun/utils</url>
    <licenses>
        <license>
            <name>GNU GENERAL PUBLIC LICENSE, Version 3.0</name>
            <url>https://www.gnu.org/licenses/gpl-3.0.txt</url>
        </license>
    </licenses>
    <developers>
        <developer>
            <name>luoaijun</name>
            <email>aijun.luo@outlook.com</email>
            <organization>luoaijun</organization>
            <organizationUrl>https://github.com/luoaijun</organizationUrl>
            <roles>
                <role>Developer</role>
            </roles>
            <timezone>+8</timezone>
        </developer>
    </developers>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.build.reportingEncoding>UTF-8</project.build.reportingEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>
    <scm>
        <connection>scm:git:https://github.com/luoaijun/utils.git</connection>
        <developerConnection>scm:git:https://github.com/luoaijun/utils.git</developerConnection>
        <url>https://github.com/luoaijun/utils</url>
        <tag>HEAD</tag>
    </scm>
    <repositories>
        <repository>
            <id>ossrh</id>
            <name>Open Source Project Repository Hosting</name>
            <url>https://oss.sonatype.org/content/groups/public</url>
        </repository>
    </repositories>
    <distributionManagement>
        <snapshotRepository>
            <id>ossrh</id>
            <url>https://oss.sonatype.org/content/repositories/snapshots</url>
        </snapshotRepository>
        <repository>
            <id>ossrh</id>
            <url>https://oss.sonatype.org/service/local/staging/deploy/maven2</url>
        </repository>
    </distributionManagement>
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-clean-plugin</artifactId>
                <version>3.0.0</version>
            </plugin>
            <plugin>
                <artifactId>maven-resources-plugin</artifactId>
                <version>3.0.2</version>
            </plugin>
            <plugin>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.7.0</version>
            </plugin>
            <plugin>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.20.1</version>
            </plugin>
            <plugin>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.0.2</version>
            </plugin>
            <plugin>
                <artifactId>maven-install-plugin</artifactId>
                <version>2.5.2</version>
            </plugin>
            <plugin>
                <artifactId>maven-deploy-plugin</artifactId>
                <version>2.8.2</version>
            </plugin>
            <plugin>
                <groupId>org.sonatype.plugins</groupId>
                <artifactId>nexus-staging-maven-plugin</artifactId>
                <version>1.6.8</version>
                <extensions>true</extensions>
                <configuration>
                    <serverId>ossrh</serverId>
                    <nexusUrl>https://oss.sonatype.org/</nexusUrl>
                    <autoReleaseAfterClose>true</autoReleaseAfterClose>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>lint</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-compiler-plugin</artifactId>
                        <version>3.7.0</version>
                        <configuration>
                            <compilerArgs>
                                <arg>-Xlint:unchecked</arg>
                            </compilerArgs>
                        </configuration>
                    </plugin>
                </plugins>
            </build>
        </profile>

        <profile>
            <id>release</id>
            <activation>
                <property>
                    <name>release</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-javadoc-plugin</artifactId>
                        <version>3.0.1</version>
                        <executions>
                            <execution>
                                <id>attach-javadocs</id>
                                <goals>
                                    <goal>jar</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-source-plugin</artifactId>
                        <version>3.0.1</version>
                        <executions>
                            <execution>
                                <id>attach-sources</id>
                                <goals>
                                    <goal>jar</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-gpg-plugin</artifactId>
                        <version>1.6</version>
                        <executions>
                            <execution>
                                <id>sign-artifacts</id>
                                <phase>verify</phase>
                                <goals>
                                    <goal>sign</goal>
                                </goals>
                                <configuration>
                                    <passphraseServerId>gpg.passphrase</passphraseServerId>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
            <reporting>
                <plugins>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-javadoc-plugin</artifactId>
                        <version>3.0.1</version>
                    </plugin>
                </plugins>
            </reporting>
        </profile>

        <profile>
            <id>default</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <build>
                <defaultGoal>compile</defaultGoal>
                <plugins>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-source-plugin</artifactId>
                        <version>2.2.1</version>
                        <executions>
                            <execution>
                                <phase>package</phase>
                                <goals>
                                    <goal>jar-no-fork</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-javadoc-plugin</artifactId>
                        <version>2.9.1</version>
                        <executions>
                            <execution>
                                <phase>package</phase>
                                <goals>
                                    <goal>jar</goal>
                                </goals>

                                <configuration>
                                    <additionalparam>-Xdoclint:none</additionalparam>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-gpg-plugin</artifactId>
                        <version>1.6</version>
                        <executions>
                            <execution>
                                <phase>verify</phase>
                                <goals>
                                    <goal>sign</goal>
                                </goals>
                                <configuration>
                                    <passphraseServerId>gpg.passphrase</passphraseServerId>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
            <distributionManagement>
                <snapshotRepository>
                    <id>ossrh</id>
                    <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
                </snapshotRepository>
                <repository>
                    <id>ossrh</id>
                    <url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
                </repository>
            </distributionManagement>
        </profile>
    </profiles> 
</project>
```


#### 7. Publish jar package
> The first time you execute the MVN clean deploy command, you need to enter the password of the GPG key

```
>mvn clean deploy
```

#### 8. Close and release
> If you refer to my POM file, it will automatically close and release.
- else login by this url and go to close:

**URL:**[https://oss.sonatype.org/#stagingRepositories](https://oss.sonatype.org/#stagingRepositories)

#### 9. End like this 

- When all the preparations have been completed ,<issues@sonatype.org> will email to you。Like this：


```
Central sync is activated for com.luoaijun. 
After you successfully release, your component will be published to Central, typically within 10 minutes, though updates to search.maven.org can take up to two hours.
```
