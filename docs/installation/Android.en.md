# Install on Android #

You can install the SDK using Artifactory as Maven repository.
To authenticate you have to put your credentials in the app **gradle.properties** file:

#### gradle.properties

```gradle
artifactory_user={username}
artifactory_password={password}
```

Then in the app **build.gradle** file add the repository address:

#### app/build.gradle

```gradle
repositories {

    ...

    maven {
        url "https://d314astu88ufzo.cloudfront.net/artifactory/gradle-release-local"
        credentials(PasswordCredentials) {
            username "${artifactory_user}"
            password "${artifactory_password}"
        }
    }
}
```

Finally add **Conio SDK** as app dependency:

#### app/build.gradle

```gradle
dependencies {

    ...

    implementation 'com.conio:sdk2:[VERSION]'
}
```

Then just sync Gradle files.