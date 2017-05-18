# Simple TestNG Class {#simple-testng-class}

Create a New Class Named SimpleTestNGClassExample in Eclipse. and copy paste the below code to the class. Run the Script by right Clicking anywhere in the code editor and click "Run As" &gt; TestNG Test. Please note the option "Run As &gt; TestNG" won't appear if you don't have testNG plugins. Follow this tutorial to install testng plugins.

```
package com.selenium;

import org.testng.annotations.Test;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.AfterTest;

public class SimpleTestNGClassExample {

    @BeforeTest
    public void initialization() {
        System.out.println("This method will be executed once before the"
                + "testMethod gets called..");
        System.out.println("All the statements like browser setup, "
                + "data-variable Initilization etc. should be done here..");
    }

    @Test
    public void testMethod() {
        System.out.println("This method will be called after the setup method"
                + "is called..");
        System.out.println("All the statements related to test execution"
                + "Should appear here..");
    }

    @AfterTest
    public void cleanup() {
        System.out
                .println("This method will be called after all previous methods"
                        + "are executed..");
        System.out.println("All the statements related to clean up activity"
                + "or closure activity should be listed here..");
    }

}

```

Testng works by looking for Annotation in the code, name @BeforeTest, @Test, @AfterTest and so on. The code in these annotations is run sequentially.

