# Internet Explorer Profile for Selenium WebDriver {#proxies-profiles-certificates}

---

Some of the Profile settings for Internet Explorer Driver are mentioned in the below snippet.

```
package code;

import java.io.File;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.Proxy;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.ie.InternetExplorerDriver;
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

        // Below code for the Internet Explorer capability 
       DesiredCapabilities ieCapabilities = DesiredCapabilities.internetExplorer();
        // Set ACCEPT_SSL_CERTS variable to true
        ieCapabilities.setCapability(CapabilityType.ACCEPT_SSL_CERTS, true);
        //To set the proxy to auto detect network settings
        ieCapabilities.setCapability("network.proxy.type", ProxyType.AUTODETECT.ordinal());
        //Added to avoid the Protected Mode settings for all zones
        ieCapabilities.setCapability(InternetExplorerDriver.INTRODUCE_FLAKINESS_BY_IGNORING_SECURITY_DOMAINS, true); 
        ieCapabilities.setCapability(InternetExplorerDriver.INITIAL_BROWSER_URL, "about:blank");
        ieCapabilities.setCapability(InternetExplorerDriver.SILENT, true);
        ieCapabilities.setCapability(InternetExplorerDriver.IE_ENSURE_CLEAN_SESSION, true);
        ieCapabilities.setCapability(InternetExplorerDriver.IGNORE_ZOOM_SETTING,true);
        System.setProperty("webdriver.ie.driver","C:\\SaiKiran\\Drivers\\IEDriverServer.exe");
        //Add Pop-up allowed in IE manually
        driver = new InternetExplorerDriver(ieCapabilities);
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



