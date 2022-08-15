# LoadRunner-with-Appium-Example

In this example we will briefly look at how we can use LoadRunner with Appium to run Performance Tests

## Prerequisites

- 32-bit JDK Version for LoadRunner support of Java Vusers
- LoadRunner installed locally on your Windows machine

## Initial Setup

Let's see how we can create a script in Virtual User Generator

1. In the "Create a New Script" window, select & create Java Vuser, a new file will be created under the name Actions.java
2. Try running the script to ensure no issues with compilation. If you run into compiling errors, it could be that the JDK is not properply configured
  a. In the Solution Explorer, go to Runtime Settings
  b. In the Settings tab, provide path to your 32-bit JDK version
  c. Run again to verify no compiling issues
  
## Adding Dependencies

In order to run Appium scripts, we need Dependencies to be able to reference during run-time. Find a [list of all dependencies here]([insert link](https://loadrunnerdependencies.s3.us-east-2.amazonaws.com/loadrunner_dependencies.zip)).
In the Runtime Settings Tab, add the .jar files:



## Adding the Script

```
Code to be added
```
