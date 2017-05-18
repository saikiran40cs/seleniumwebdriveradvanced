# Opera Profile for Selenium WebDriver {#proxies-profiles-certificates}

---

Some of the Profile settings for Opera Driver are mentioned in the below snippet.

```
package code;

import java.io.File;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.Proxy;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.opera.OperaDriver;
import org.openqa.selenium.opera.OperaOptions;
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

        // Below code for the Opera capability 
        OperaOptions operaOptions = new OperaOptions();
        DesiredCapabilities OperaCapabilities = DesiredCapabilities.chrome();
        OperaCapabilities.setCapability(ChromeOptions.CAPABILITY, operaOptions);
        OperaCapabilities.setCapability("network.proxy.type", proxyType);
        
        // Set ACCEPT_SSL_CERTS variable to true
        OperaCapabilities.setCapability(CapabilityType.ACCEPT_SSL_CERTS, true);

        System.setProperty("webdriver.opera.driver",OPERADRIVERPATH);
        System.setProperty("opera.arguments", "--disable-logging");
        System.setProperty("webdriver.opera.silentOutput", "true");
        
        driver = new OperaDriver(OperaCapabilities);
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



