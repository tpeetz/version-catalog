# version-catalog
Version-Catalog to use in Gradle projects.


## Usage

The documentation about version catalogs can be found in Gradle [docs](https://docs.gradle.org/current/userguide/platforms.html#sec:importing-published-catalog).

You need to create version catalogs in `settings.gradle` from remote repository:

```groovy
pluginManagement {
    repositories {
        maven {
            name = "GitHubPackages"
            url "https://maven.pkg.github.com/tpeetz/version-catalog"
            credentials(PasswordCredentials)
        }
        gradlePluginPortal()
    }
}
dependencyResolutionManagement {
	repositories {
        maven {
            name = "GitHubPackages"
            url "https://maven.pkg.github.com/tpeetz/version-catalog"
            credentials(PasswordCredentials)
        }
    }

    versionCatalogs {
        create("versionsLibs") {
            from("de.tpeetz:version-catalog:1.0.0-SNAPSHOT")
        }
    }
}
```

After sync the project gradle create accessors for dependencies like:

```groovy
plugins {
    alias(versions.plugins.libraryConvention)
    alias(versions.plugins.asciidoctorConvention)
    alias(versions.plugins.sonarqube)
}

dependencies {
    implementation versions.slf4j
    testImplementation versions.mockito
    testImplementation versions.junit
    implementation versions.bundles.logback
}
```
