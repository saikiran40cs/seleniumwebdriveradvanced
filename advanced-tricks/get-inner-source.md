# Get HTML Source of WebElement {#simple-testng-class}

---

This situation generally arises whenever developers require more inputs which has caused the issue.

To apprehend the problem we are using the GetAttribute  method of the IWebElement interface to get the inner HTML of a specific element.

```
public void GetHtmlSourceOfWebElement()
{
  driver.get("https://saikiranpro.blogspot.in");
  WebElement element = driver.findElement(By.xpath("//h3[text()='About Me']"));
  string sourceHtml = element.getAttribute("innerHTML");
  System.out.println(sourceHtml);
}
```

The entire output in console can be sent to developer as-is.

