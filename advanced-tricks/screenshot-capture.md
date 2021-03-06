# Screenshot capture {#simple-testng-class}

---

This situation generally arises whenever there is a failure in the application. This will help developers know the areas of changes which has caused the issue.

To apprehend the problem we are using the Interface ITakesScreenshot method to take a full-screen screenshot of the browser in required format.

**In .NET**

```
public void TakeFullScreenshot(IWebDriver driver, String filename)
{
    Screenshot screenshot = ((ITakesScreenshot)driver).GetScreenshot();
    screenshot.SaveAsFile(filename, ImageFormat.Png);
}
```

Sometimes you may need to take a screenshot of a single element.

```
public void TakeScreenshotOfElement(IWebDriver driver, By by, string fileName)
{
 // 1. Make screenshot of all screen
 var screenshotDriver = driver as ITakesScreenshot;
 Screenshot screenshot = screenshotDriver.GetScreenshot();
 var bmpScreen = new Bitmap(new MemoryStream(screenshot.AsByteArray));

 // 2. Get screenshot of specific element
 IWebElement element = driver.FindElement(by);
 var cropArea = new Rectangle(element.Location, element.Size);
 var bitmap = bmpScreen.Clone(cropArea, bmpScreen.PixelFormat);
 bitmap.Save(fileName);
}
```

First we make a full-screen screenshot then we locate the specified element by its location and size attributes. After that, the found rectangle chunk is saved as a bitmap.

Here is how you use both methods in tests.

```
@AfterMethod
public void WebDriverAdvancedUsage_TakingFullScrenenScreenshot()
{
 this.driver.Navigate().GoToUrl(@"https://saikiranpro.blogspot.in/");
 this.WaitUntilLoaded();
 string tempFilePath = Path.GetTempFileName().Replace(".tmp", ".png");
 this.TakeFullScreenshot(this.driver, tempFilePath);
}

@AfterMethod
public void WebDriverAdvancedUsage_TakingElementScreenshot()
{
 this.driver.Navigate().GoToUrl(@"https://saikiranpro.blogspot.in/");
 this.WaitUntilLoaded();
 string tempFilePath = Path.GetTempFileName().Replace(".tmp", ".png");
 this.TakeScreenshotOfElement(this.driver,By.XPath("//h3[text()='About Me ']"), tempFilePath);
}
```

We get a temp file name through the special "Path" .NET class. By default temp files are generated with ".tmp" extension because of that we replace it with ".png".

