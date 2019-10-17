# interlok-build-parent

The suggested name was bookish-parakeet.

## Usage

```
// build.gradle
ext {
    version = project.hasProperty('version') ? project.getProperty('version') : '0.0.0'
    interlokVersion = project.hasProperty('interlokVersion') ? project.getProperty('interlokVersion') : '3.9.1-RELEASE'
    interlokParentGradle = project.hasProperty('interlokParentGradle') ? project.getProperty('interlokParentGradle') : "https://raw.githubusercontent.com/adaptris-labs/interlok-build-parent/${interlokVersion}/parent.gradle"
}

allprojects {
    apply from: "${interlokParentGradle}"
}

dependencies { 
    interlokRuntime ("com.adaptris:interlok-json:$interlokVersion") { changing=true }
    interlokRuntime ("com.adaptris:interlok-filesystem:$interlokVersion") { changing=true }
    interlokRuntime ("com.adaptris:interlok-csv-json:$interlokVersion") { changing=true }
}
```

## Check

Executes:
 * Config test
 * Service Tester
 * Version Report

```
gradle clean check 
```

## Assemble

Build lib and config directory in : `./build/distribution`

```
gradle clean assemble
```
