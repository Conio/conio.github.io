# Installazione su Android #

L'SDK si installa utilizzando il repository Maven di Artifactory.
Per potersi autenticare al repository è necessario configurare le credenziali nel file **gradle.properties** come segue:

#### gradle.properties

```gradle
artifactory_user={username}
artifactory_password={password}
```

A questo punto sarà possibile aggiungere l'indirizzo del repository nel **build.gradle** dell'applicazione:

#### app/build.gradle

```gradle
repositories {

    ...

    maven {
        url "https://artifactory.conio.com/artifactory/gradle-release-local"
        credentials(PasswordCredentials) {
            username "${artifactory_user}"
            password "${artifactory_password}"
        }
    }
}
```

Dopo aver specificato l'indirizzo del repository dal quale verranno sincronizzati gli artefatti sarà possibile aggiungere il **Conio SDK** come dipendeza dell'applicazione:

#### app/build.gradle

```gradle
dependencies {

    ...

    implementation 'com.conio:sdk2:[VERSION]'
}
```

Sincronizzando il progetto con Gradle sarà possibile utilizzare l'SDK.