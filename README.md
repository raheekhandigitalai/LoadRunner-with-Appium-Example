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

In order to run Appium scripts, we need Dependencies to be able to reference during run-time. Find the [list of all dependencies here.](https://loadrunnerdependencies.s3.us-east-2.amazonaws.com/loadrunner_dependencies.zip)

In the Runtime Settings Tab, add the .jar files:

![image](https://user-images.githubusercontent.com/71343050/184656181-d13f401f-639d-4590-a0e6-14d7e0e07669.png)

We now also need to add dependency references into Actions.java so that the script can reach the dependencies during runtime:

```
importlrapi.lr;

import io.appium.java_client.ios.IOSDriver;
import io.appium.java_client.ios.IOSElement;
import io.appium.java_client.remote.IOSMobileCapabilityType;
import io.appium.java_client.remote.MobileCapabilityType;
import org.openqa.selenium.By;
import org.openqa.selenium.ScreenOrientation;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.net.MalformedURLException;
import java.net.URL;
```

![image](https://user-images.githubusercontent.com/71343050/184657014-42759ee0-0c05-4c76-ad7f-a8598f3fdc70.png)

## Adding the Script

```
Code to be added
```
