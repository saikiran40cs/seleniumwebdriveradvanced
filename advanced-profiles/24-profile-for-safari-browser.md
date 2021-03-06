# Safari Profile for Selenium WebDriver {#proxies-profiles-certificates}

---

Some of the Profile settings for Safari Driver are mentioned in the below snippet.

```
package code;

import java.io.File;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.Proxy;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.safari.SafariDriver;
import org.openqa.selenium.safari.SafariOptions;
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

        // Below code for the safari capability
        SafariOptions safariOptions=new SafariOptions();
        DesiredCapabilities SafariCapabilities = DesiredCapabilities.safari();
        SafariCapabilities.setCapability(SafariOptions.CAPABILITY, safariOptions);

        // Set ACCEPT_SSL_CERTS variable to true
        SafariCapabilities.setCapability(CapabilityType.ACCEPT_SSL_CERTS, true);
        //To set the proxy to auto detect network settings
        SafariCapabilities.setCapability("network.proxy.type", ProxyType.AUTODETECT.ordinal());
        driver = new SafariDriver(SafariCapabilities);
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



