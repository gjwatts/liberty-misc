# Repo for quick testing of Liberty apps
Especially for new JUD (Java Under Development - a.k.a pre-release or early access) versions.

### For versions of Java that already have gradle support 

To build+run locally:

```
./gradlew start
```

Or to just build locally:

```
./gradlew build
```

---

### For versions of Java that do not have gradle support yet
Make the following updates in the following files (example given here as if you were working with pre-gradle support for Java 16):

- In **gradle.properties**, set:

```
org.gradle.java.installations.fromEnv=JDK16
```

where JDK16 is a system environment variable that reflects the location of your Java 16 JDK you wish the source to be complied at (see last step).


- In **build.gradle**, set:

```
   languageVersion = JavaLanguageVersion.of(16)
```

- And then set the environment variable JDK16 to your Java 16 JDK home

Example (for Java 16):

```
(Mac)      export JDK16="/path/to/your/jdk16/home"
(Unix)     JDK16="/path/to/your/jdk16/home"
(Win DOS)  set JDK16="C:\path\to\your\jdk16\home"
(Win PS)   $env:JDK16="C:\path\to\your\jdk16\home"
```

- Then, to build the WAR file locally:

```
./gradlew build
```

---

### When moving to a new release of Java

Here are the locations to bump up the release number to the current java version

- org.eclipse.wst.common.component

```
    version = '1.16-SNAPSHOT'
    appUrl = 'http://localhost:9080/java16-app/'
```
  
- settings.gradle

```
    rootProject.name = 'java16-app' 
```

- gradle-wrapper.properties (might as well bump up to the latest supported version of gradle)

```
	distributionUrl=https\://services.gradle.org/distributions/gradle-X.Y-bin.zip
```

Then add new code to `TestServices.java` either directly or via another class.
