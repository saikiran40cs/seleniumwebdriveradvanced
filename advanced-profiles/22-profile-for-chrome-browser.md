# Chrome Profile for Selenium WebDriver {#proxies-profiles-certificates}

---

Some of the Profile settings for Chrome Driver are mentioned in the below snippet.

```
package code;

import java.io.File;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.Proxy;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.remote.CapabilityType;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

public class ProxiesCertificates {
    WebDriver driver;
    String baseUrl;

    @BeforeTest
    public void setup() {

        // Below code for the chrome capability 
        ChromeOptions chromeOptions = new ChromeOptions();
        DesiredCapabilities ChromeCapabilities = DesiredCapabilities.chrome();
        ChromeCapabilities.setCapability(ChromeOptions.CAPABILITY, chromeOptions);
        ChromeCapabilities.setCapability("network.proxy.type", proxyType);
        
        // Set ACCEPT_SSL_CERTS variable to true
        ChromeCapabilities.setCapability(CapabilityType.ACCEPT_SSL_CERTS, true);
        ChromeCapabilities.setCapability(CapabilityType.ForSeleniumServer.ENSURING_CLEAN_SESSION, true); 
        
        Map<String, Object> prefs = new HashMap<String, Object>();
        prefs.put("profile.default_content_settings.popups", 0);
        prefs.put("download.extensions_to_open", "pdf"); 
        //prefs.put("--always-authorize-plugins",true);
        prefs.put("download.prompt_for_download", "true");
        prefs.put("download.default_directory", DOWNLOADPATH);
        
        chromeOptions.setExperimentalOption("prefs", prefs);
        
        System.setProperty("webdriver.chrome.driver",CHROMEDRIVERPATH);
        System.setProperty("webdriver.chrome.args", "--disable-logging");
        System.setProperty("webdriver.chrome.silentOutput", "true");
        
        driver = new ChromeDriver(ChromeCapabilities);
        driver.manage().timeouts().implicitlyWait(50, TimeUnit.SECONDS);
        driver.manage().deleteAllCookies();
        driver.manage().window().maximize();
    }

    @Test
    public void testMethod() {
        baseUrl = "http://docs.seleniumhq.org/";
        driver.get(baseUrl);
    }

    @AfterTest
    public void teardown() {
        driver.quit();
    }

}
```



