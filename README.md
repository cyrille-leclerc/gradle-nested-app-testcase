
# Gradle Nested App TestCase

The purpose of this test case is to show how a parent application project `my-parent-app-1.0-SNAPSHOT.zip` can easily
embed a child zip application project `my-nested-app-1.0-SNAPSHOT.zip`.

It is easy to have a parent app project `my-parent-app-1.0-SNAPSHOT.zip` embedding the child generated jar file
`my-nested-app-1.0-SNAPSHOT.jar`.

How can I


## Parent `build.gradle` fragment


```json
configurations {
    applicationDependencies
}


dependencies {
    compile 'args4j:args4j:2.0.26'

    // QUESTION: how can I reference the generated my-nested-app-1.0.zip file instead of ?
    applicationDependencies project(path: ':my-nested-app')
    applicationDependencies 'org.apache.tomcat:tomcat:8.0.0-RC10@zip'
}

// embed the dependencies declared with "applicationDependencies" into the "dist" dir of the generated application
applicationDistribution.from(configurations.applicationDependencies) {
    into "dist"
}

```

## Project directory structure

```
my-parent-app
├── build
│   ├── distributions
│   │   └── my-parent-app-1.0-SNAPSHOT.zip
│   ├── libs
│   │   └── my-parent-app-1.0-SNAPSHOT.jar
│   └── ...
├── my-nested-app
│   ├── build
│   │   ├── distributions
│   │   │   └── my-nested-app-1.0-SNAPSHOT.zip
│   │   ├── libs
│   │   │   └── my-nested-app-1.0-SNAPSHOT.jar
│   │   └── ...
│   ├── build.gradle
│   └── src
│       └── main
│           └── java
│               └── ...
├── settings.gradle
└── src
    └── main
        └── java
            └── ...
```