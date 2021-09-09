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
Make the following updates in the following files (example given here as if you were working with pre-gradle support for Java 17):

- In **gradle.properties**, set:

```
org.gradle.java.installations.fromEnv=JDK17
```

where JDK17 is a system environment variable that reflects the location of your Java 17 JDK you wish the source to be complied at (see last step).


- In **build.gradle**, set:

```
   languageVersion = JavaLanguageVersion.of(17)
```

- And then set the environment variable JDK17 to your Java 17 JDK home

Example (for Java 17):

```
(Mac)      export JDK17="/path/to/your/jdk17/home"
(Unix)     JDK17="/path/to/your/jdk17/home"
(Win DOS)  set JDK17="C:\path\to\your\jdk17\home"
(Win PS)   $env:JDK17="C:\path\to\your\jdk17\home"
```

- Then, to build the WAR file locally:

```
./gradlew build
```

---

### When moving to a new release of Java

Here are the locations to bump up the release number to the current Java version

- **org.eclipse.wst.common.component** (in the `.settings` directory)

```
<wb-module deploy-name="java17-app">
		<property name="context-root" value="java17-app"/>
```

- **build.gradle**

```
    version = '1.17-SNAPSHOT'
    appUrl = 'http://localhost:9080/java17-app/'
    
    <Make sure to add any new dependencies or update existing ones to the proper levels>
```
  
- **settings.gradle**

```
    rootProject.name = 'java17-app' 
```

- **gradle-wrapper.properties** (might as well bump up to the latest supported version of gradle)

```
	distributionUrl=https\://services.gradle.org/distributions/gradle-X.Y-bin.zip
```

Then add new code to **TestServices.java** either directly or via another class and make sure **TestApp.java** is in the same directory as it.
