# interlok-build-parent

The suggested name was bookish-parakeet.

## Usage

```
// build.gradle
ext {
    interlokVersion = '3.9.2-RELEASE'
    interlokParentGradle = "https://raw.githubusercontent.com/adaptris-labs/interlok-build-parent/${interlokVersion}/parent.gradle"
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
