# LoadRunner with Appium Example

In this example we will look at how we can use LoadRunner to run Performance Tests with Appium against [Digital.ai's Continuous Testing platform](https://digital.ai/continuous-testing).

- [Prerequisites](#Prerequisites)
- [Initial Setup](#Initial-Setup)
- [Adding Dependencies](#Adding-Dependencies)
- [Adding the Script](#Adding-the-Script)
- [References](#References)

## Prerequisites

- 32-bit JDK Version for LoadRunner support of Java Vusers
- LoadRunner installed locally on your Windows machine

## Initial Setup

Let's see how we can create a script in **Virtual User Generator**

1. In the "Create a New Script" window, select & create Java Vuser, a new file will be created under the name **Actions.java**

![image](https://user-images.githubusercontent.com/71343050/184699859-38371e1d-8eb6-404f-b124-c972a7331e6e.png)

2. Try running the script to ensure no issues with compilation. If you run into compiling errors, it could be that the JDK is not properply configured

    a. In the Solution Explorer, go to Runtime Settings
  
    b. In the Settings tab, provide path to your 32-bit JDK version
  
    c. Run again to verify no compiling issues
  
## Adding Dependencies

In order to run Appium scripts, we need Dependencies to be able to reference during run-time. Find the [list of all dependencies here.](https://loadrunnerdependencies.s3.us-east-2.amazonaws.com/loadrunner_dependencies.zip)

In the Runtime Settings Tab, add the .jar files:

![image](https://user-images.githubusercontent.com/71343050/184656181-d13f401f-639d-4590-a0e6-14d7e0e07669.png)

We now also need to add dependency references into **Actions.java** so that the script can reach the dependencies during runtime:

```
import lrapi.lr;

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

For this example, we'll look at running a simple Appium Script on an iOS Device with a Native Application.
For the code logic, we need to add it under the "action" function:

```
public int action() throws Throwable {

  DesiredCapabilities capabilities = newDesiredCapabilities();
  capabilities.setCapability("accessKey", "<INSERT_ACCESS_KEY>");
  capabilities.setCapability("udid", "00008020-000C24C61A60802E");
  capabilities.setCapability("testName", "LoadRunner With Appium Integration");
  capabilities.setCapability("bundleId", "com.experitest.ExperiBank");
  
  IOSDriver driver = newIOSDriver(newURL("https://uscloud.experitest.com/wd/hub"), capabilities);
  
  try {
    newWebDriverWait(driver,5).until(ExpectedConditions.elementToBeClickable(By.name("usernameTextField")));
    driver.findElement(By.name("usernameTextField")).sendKeys("company");
    driver.findElement(By.name("passwordTextField")).sendKeys("company");

    lr.start_transaction("Login to ExperiBank"); //Creates a transaction in loadrunner
    
    driver.findElement(By.name("loginButton")).click();
    newWebDriverWait(driver,5).until(ExpectedConditions.elementToBeClickable(By.name("logoutButton")));
    
    lr.end_transaction("Login to ExperiBank",lr.AUTO); //Match this with the start_transaction
  } catch (Exception e) {
  
  } finally {
    try {
        driver.quit();
    } catch (Exception e) {
        e.printStackTrace();
    }
  }
return0;
}
```

In this example, we are launching an Application by the Bundle ID, entering credentials into the username and password field, and before clicking on Login, I am starting the transaction from LoadRunner, and ending the transaction once I am logged in and successfully landed on the dashboard page.

## Viewing the Test Execution and Results in Digital.ai's Continuous Testing platform

While the test is being executed, we would be able to see the live test running under **Execution** page:

![image](https://user-images.githubusercontent.com/71343050/184659393-e6a3d078-63d1-4dbf-bf55-fc10a99bc544.png)

Once the functional test is finished, a report is generated under the **Reports** page:

![image](https://user-images.githubusercontent.com/71343050/184659675-cb4d977f-b93a-4589-8495-756e8d83c6af.png)

By clicking on the relevant report, we can see a detailed reference of the functional test:

![image](https://user-images.githubusercontent.com/71343050/184659847-7f6392d8-ad44-44ba-b91c-6f77335167cc.png)

## References

[Obtain your Access Key](https://docs.experitest.com/display/TE/Obtaining+Access+Key)

[Appium Capabilities](https://docs.experitest.com/display/TE/Appium+Server+%28Open+Source%29+Execution)
