# Artifact Repository Manager with Nexus

## Table of Contents

- [Create Ubuntu Server (Droplet)](#create-ubuntu-server-droplet)
    - [Configuration](#configuration)
- [Open Ports](#open-ports)
- [Install Java](#install-java)
- [Download and Install Nexus](#download-and-install-nexus)
- [Create User and Group](#create-user-and-group)
- [Start Nexus Server](#start-nexus-server)
- [Check on Browser](#check-on-browser)
- [Login with Default User](#login-with-default-user)
- [Create New Nexus User and Role](#create-new-nexus-user-and-role)
- [Configure the Gradle Project with Nexus](#configure-the-gradle-project-with-nexus)
    - [In build.gradle](#in-buildgradle)
    - [Build Project](#build-project)
    - [Publish Project Using Gradle Publish Plugin](#publish-project-using-gradle-publish-plugin)
- [Maven Configuration in pom.xml](#maven-configuration-in-pomxml)
- [Build and Deploy](#build-and-deploy)

## create ubuntu server (droplet)
### configuration
- 4 GB RAM
- 2 CPUs
- 160 GB SSD Disk

## open ports
- open port 22 as an inbound rule
- open port 8081 as an inbound rule

## install java
```bash
apt install openjdk-25-jre-headless
```

## download and install Nexus
```bash
download zip and unzip it
https://help.sonatype.com/en/download.html
```

## create user and group
- create nexus user
- set rights (chown -R nexus:nexus <folder>)

## start nexus server
```bash
/opt/nexus.../bin/nexus start
```

## check on browser
- https://droplet-IP:8081/

## login with default user
- admin user

## create new nexus user and role
- in nexus go to settings>security>roles
- create new Role
- apply maven-snapshot-* roles

- in nexus go to settings>security>users
- create new user
- assign new role to user


# configure the gradle project with nexus
## in build.gradle
- add plugin
```bash
  apply plugin: 'maven-publish'
```
- add publishing
```groovy
publishing {
    publications {
        create("maven", MavenPublication) {
            artifact("build/libs/my-app-$version" + ".jar") {
                extension = 'jar'
            }
        }
    }

    repositories {
        maven {
            name = 'nexus'
            url = "http://droplet-ip/repository/maven-snapshots/"
            allowInsecureProtocol = true
            credentials {
                username = project.repoUser
                password = project.repoPassword
            }
        }
    }
}
```

- add gradle.properties for username and passwords

## build project
```bash
gradle build
```


## publish project using gradle publish plugin
```bash
gradle publish
```
- check in nexus that the artifact has been transferred

## maven configuration in pom.xml
1. add plugin
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-deploy-plugin</artifactId>
    <version>3.1.4</version>
</plugin>
```

2. add repo endpoint
```xml
<distributionManagement>
    <snapshotRepository>
        <id>nexus-snapshots</id>
        <url>http://${repo.ip}:${repo.port}/repository/maven-snapshots</url>
    </snapshotRepository>
</distributionManagement>
```

3. create .m2 settings.xml
```xml
<settings>
  <servers>
    <server>
     <id>nexus-snapshots</id>
     <username>user</username>
     <password>pw</password>
    </server>
  </servers>
</settings>
```

## build and deploy
- go to project
```bash
mvn package
```

```bash
mvn deploy
```
