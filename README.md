# interlok-build-parent

The suggested name was bookish-parakeet.

This is a gradle file that can be applied to your gradle file to simplify things bootstrapping your Interlok project. Gradle 5.x+ is required.

## Usage

```
// build.gradle
ext {
  interlokParentGradle = "https://raw.githubusercontent.com/adaptris-labs/interlok-build-parent/master/build.gradle"
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

Or you can override version:

```
// build.gradle
ext {
  interlokVersion = '3.9.2-RELEASE'
  interlokUiVersion = interlokVersion
  interlokParentGradle = "https://raw.githubusercontent.com/adaptris-labs/interlok-build-parent/master/build.gradle"
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

A full example with configuration is here : [build-parent-json-csv](https://github.com/adaptris-labs/build-parent-json-csv)

## Gradle Tasks

* `gradle clean check` will verify the configuration unmarshalls; execute service-tester if `src/test/interlok/service-test.xml` exists; and finally runs a version report.
* `gradle clean assemble` will build your distribution, you end up with an Interlok installed into `./build/distribution`
* `gradle clean build` will execute both the steps above

## Next steps

```
cd ./build/distribution
java -jar lib/interlok-boot.jar
```

## The bit you probably won't read; but you should.

* You probably want to run clean every time before a build because of the way gradle detects up-to-date files.
* Because we have custom closures that resolve dependencies (i.e. interlokRuntime); you need to apply from the parent *after all your dependencies are declared* otherwise you get an error.


### Customising your build

There is support for build environments; you can pass in a gradle property to specify the build environment `gradle -PbuildEnv=myEnv clean check`. What this does is to copy the file `variables-local-{buildenv}.properties` to variables-local.properties so that you can potentially override various settings on a per build basis. If the `buildEnv` is set to the _dev_ then the service tester jars are copied into the distribution in the expectation that you will be using the UI service tester page.

If you don't want to assemble into `./build/distribution` then you can override that location by defining a `interlokDistDirectory=` in your gradle properties (or on the commandline). We generally discourage this, unless you are only running the assemble task.

