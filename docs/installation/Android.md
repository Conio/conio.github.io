# Android Installation

## Prerequisites
---

- Min Android SDK: 23 (Android 6.0 “Marshmallow”)

## Installation
---
The Conio Android SDK is located in a private Maven repository on *JFrog Artifactory*, so it is necessary to configure the authentication as follow.

- Add the Artifactory credentials provided by Conio to your global `gradle.properties`
```
artifactory_user=<username provided by Conio>
artifactory_password=<password provided by Conio>
```

- Add the Conio Artifactory repository to your `build.gradle`
```
repositories {
    // ...
    maven {
        url "https://artifactory.conio.com/artifactory/gradle-release-local"
        credentials(PasswordCredentials) {
            username "${artifactory_user}"
            password "${artifactory_password}"
        }
    }
}
```
- Add the Conio SDK dependency
```
dependencies {
    // ...
    implementation 'com.conio:sdk-b2b:[VERSION]'
}
```
