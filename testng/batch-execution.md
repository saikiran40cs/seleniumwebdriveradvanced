# Execution of tests from batch file {#simple-testng-class}

---

We will see how does one make use of TestNG to Execution of tests from batch file.

First one needs to set the JAVA\_HOME in the system environment variables so that we can run the tests using the batch file.

Set the classpath of java so that the compilation can be done using command prompt.

Save the below batch code in a  new file and save it as "RunBatchtests.cmd"

```
set projectLocation=C:\Saikiran\TestNGProject
cd %projectLocation%
set classpath=%projectLocation%\bin;%projectLocation%\lib\*;C:\Saikiran\Libraries\selenium-java-3.0.1\*;C:\Saikiran\Libraries\selenium-java-3.0.1\lib\*;C:\Saikiran\Libraries\extentreports-java-2.41\extentreports-java-2.41.2\*;C:\Saikiran\Libraries\extentreports-java-2.41\extentreports-java-2.41.2\lib\*;C:\Saikiran\Libraries\poi\*;

javac -cp %classpath% org.testng.TestNG %projectLocation%\smoke.xml
pause
```

After saving the file open the batch file to execute the tests from desired location.

It is a good practise to store the libraries inside the project so that we do not need to explicitly mention the libraries location instead specifying only the library folder name "lib".

The same batch can also be passed in Jenkins  jobs to execute tests from a continuous integration server.

