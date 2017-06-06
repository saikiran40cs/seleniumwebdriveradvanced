# Run Selenium in SoapUI: Groovy code

---

We can run the selenium tests in soapUI using groovy code. I have stored the chromedriver in the bin folder of SoapUI so that it can be easily accessed at the time of execution

Below is the code which can be used to run tests

```
package KiranSeleniumTest

import org.openqa.selenium.By
import org.openqa.selenium.WebDriver
import org.openqa.selenium.WebElement
import org.openqa.selenium.chrome.ChromeDriver
import org.openqa.selenium.chrome.ChromeOptions
import org.openqa.selenium.remote.CapabilityType
import org.openqa.selenium.remote.DesiredCapabilities
import org.openqa.selenium.support.ui.ExpectedCondition
import org.openqa.selenium.support.ui.WebDriverWait


// Create a new instance of the Chrome driver
ChromeOptions chromeOptions = new ChromeOptions();
DesiredCapabilities ChromeCapabilities = DesiredCapabilities.chrome();
ChromeCapabilities.setCapability(ChromeOptions.CAPABILITY, chromeOptions);					
ChromeCapabilities.setCapability(CapabilityType.ForSeleniumServer.ENSURING_CLEAN_SESSION, true); 
Map<String, Object> prefs = new HashMap<String, Object>();
prefs.put("profile.default_content_settings.popups", 0);
chromeOptions.setExperimentalOption("prefs", prefs);
System.setProperty("webdriver.chrome.driver",/C:\Program Files\SmartBear\SoapUI-5.3.0\bin\chromedriver.exe/);
System.setProperty("webdriver.chrome.args", "--disable-logging");
System.setProperty("webdriver.chrome.silentOutput", "true");

WebDriver driver =  new ChromeDriver(ChromeCapabilities);

driver.manage().window().maximize();
 
// And now use this to visit Google
driver.get("http://www.google.com");

// Find the text input element by its name
WebElement element = driver.findElement(By.name("q"));
def searchString = "cheese!"

// Enter something to search for
element.sendKeys(searchString)

// Now submit the form. WebDriver will find the form for us from the element
element.submit()

// Check the title of the page
log.info("Page title is: " + driver.getTitle())

// Google's search is rendered dynamically with JavaScript.
// Wait for the page to load, timeout after 10 seconds
(new WebDriverWait(driver, 10)).until(new ExpectedCondition() {
    public Boolean apply(WebDriver d) {
        return d.getTitle().toLowerCase().startsWith(searchString)
    }
});

// Should see: searchString" - Google Search"
log.info("Page title is: " + driver.getTitle())

//Close the browser
driver.quit()
```

We need to keep in mind that the result will be generated in the explorer and if the session is closed the results are erased.

This sample code would help you to get started on how to use selenium via soapui

