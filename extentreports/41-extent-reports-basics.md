# Basics for Extent Reports version 2

---

### Initializing Report {#initialize-report}

To initialize the report, you must create an instance of`ExtentReports`. It is possible to initialize in the following different ways:

```

var extent 
=
ExtentReports
(
string filePath
)

var extent 
=
ExtentReports
(
string filePath
,
 bool replaceExisting
)

var extent 
=
ExtentReports
(
string filePath
,
 DisplayOrder displayOrder
)

var extent 
=
ExtentReports
(
string filePath
,
 DisplayOrder displayOrder
,
 bool replaceExisting
)
```

* **filePath**
  - path of the file, in .htm or .html format
* **replaceExisting**
  - Setting to overwrite \(TRUE\) the existing file or append to it
  * True \(default\): the file will be replaced with brand new markup, and all existing data will be lost. Use this option to create a brand new report
  * False: existing data will remain, new tests will be appended to the existing report. If the the supplied path does not exist, a new file will be created.
* **displayOrder**
  * OLDEST\_FIRST \(default\) - oldest test at the top, newest at the end
  * NEWEST\_FIRST - newest test at the top, oldest at the end

### Specifying Locale {#specifying-locale}

To use a localized version \(see supported localized versions[here](http://extentreports.com/docs/versions/2/net/#localized-versions)\), use:

```

Thread
.
CurrentThread
.
CurrentUICulture 
=
 CultureInfo
.
GetCultureInfo
(
"es-ES"
)
;
// or

Thread
.
CurrentThread
.
CurrentUICulture 
=
 CultureInfo
.
GetCultureInfo
(
"es"
)
;
```

### Writing to Report {#write-to-report}

Once your session is complete and you are ready to write all logs to the report, simply call the`flush()`method.

```
// writing everything to document

extent
.
Flush
(
)
;
```

It is recommended to call`flush`only once at the end of your session because calling it multiple times will reduce the performance as the log file will be written/updated multiple times.

### Appending to an Existing Report {#append-to-report}

To append to a report you had previously created, simply mark`replaceExisting = false`and new tests will be appended to the same report.

```

ExtentReports extent 
=
new
ExtentReports
(
file
-
path
,
false
)
;
```

### Starting and Ending Tests {#start-end-tests}

To start tests, a new instance of`ExtentTest`must be created. To end, simply call`endTest(testInstance)`.

```
// new instance

var extent 
=
new
ExtentReports
(
file
-
path
)
;
// starting test

var test 
=
 extent
.
StartTest
(
"Test Name"
,
"Sample description"
)
;
// step log

test
.
Log
(
LogStatus
.
PASS
,
"Step details"
)
;
// ending test

extent
.
EndTest
(
test
)
;
// writing everything to document

extent
.
Flush
(
)
;
```

### Creating Step Logs {#create-step-logs}

There are 2 ways logs can be created: one that creates 3 columns and other that creates 4. Always use only 1 type of log for the test otherwise the table will become malformed.

```
// creates 3 columns in table: TimeStamp, Status, Details
Log
(
LogStatus
,
 Details
)
;
Log
(
LogStatus
,
 Exception
)
;
// creates 4 columns in table: TimeStamp, Status, StepName, Details
Log
(
LogStatus
,
 StepName
,
 Details
)
;
Log
(
LogStatus
,
 StepName
,
 Exception
)
;
```

### Getting Current RunStatus of Test {#current-runstatus}

You can know the current status of the test during execution by calling the`GetRunStatus()`method.

```

LogStatus status 
=
 test
.
GetCurrentStatus
(
)
;
```

### Assign Test Categories {#assign-category}

You can assign categories to tests using`AssignCategory(String... params)`method:

```

test
.
AssignCategory
(
"Regression"
)
;

test
.
AssignCategory
(
"Regression"
,
"ExtentAPI"
)
;

test
.
AssignCategory
(
"Regression"
,
"ExtentAPI"
,
"category-3"
,
"cagegory-4"
,
.
.
)
;
```

Or simply assign them when you start your test:

```

var test 
=
 extent
    
.
StartTest
(
"Categories"
)
.
AssignCategory
(
"Regression"
,
"ExtentAPI"
)
;
```

### Assign Test Author\(s\) {#assign-author}

Assign the author of the test \(similar to`AssignCategory`above\):

```

test
.
AssignAuthor
(
"Anshoo"
)
;

test
.
AssignAuthor
(
"Anshoo"
,
"Viren"
)
;
```

### Adding Child Tests {#child-tests}

To add a test node as a child of another test, use the`appendChild`method.

```

var parent 
=
 extent
.
StartTest
(
"Parent"
)
;


var child1 
=
 extent
.
StartTest
(
"Child 1"
)
;

child1
.
Log
(
LogStatus
.
Info
,
"Info"
)
;


var child2 
=
 extent
.
StartTest
(
"Child 2"
)
;

child2
.
Log
(
LogStatus
.
Pass
,
"Pass"
)
;


parent
    
.
AppendChild
(
child1
)
.
AppendChild
(
child2
)
;

    
extent
.
EndTest
(
parent
)
;
```

### Inserting custom HTML {#insert-custom-html}

Simply insert any custom HTML in the logs by using an HTML tag:

```

extent
.
Log
(
LogStatus
.
Info
,
"HTML"
,
"Usage: BOLD TEXT"
)
;
```

### Insert Snapshots {#insert-screenshots}

To add a screen-shot, simply call`addScreenCapture`. This method returns the HTML with![]()tag which can be used anywhere in the log details. Calling`addScreenCapture`will also add the image to the ImageCollectionView from where you can see all images used by your tests.

```

test
.
Log
(
LogStatus
.
Info
,
"Snapshot below: "
+
 test
.
addScreenCapture
(
"screenshot-path"
)
)
;
```

Relative paths starting with`.`and`/`are supported. If you using an absolute path,`file:///`will be automatically be appended for the image to load.

### Insert Screencast {#insert-screencast}

To add a screencast/recording of your test run, use the`addScreencast`method anywhere in the log details:

```

test
.
Log
(
LogStatus
.
Info
,
"Screencast below: "
+
 test
.
addScreencast
(
"screencast-path"
)
)
;
```

Relative paths starting with`.`and`/`are supported. If you using an absolute path,`file:///`will be automatically be appended for the screencst to load.

### Adding System Info {#add-system-info}

It is possible to add system or environment info for your using using the`AddSystemInfo`method.

```

extent
.
addSystemInfo
(
"Selenium Version"
,
"2.46"
)
;

extent
.
addSystemInfo
(
"Environment"
,
"Prod"
)
;
```

```

Dictionary si 
=
new
Dictionary
(
)
{
{
"Selenium Version"
,
"2.46"
}
,
{
"Environment"
,
"Prod"
}
}
;


extent
.
AddSystemInfo
(
si
)
;
```

### Clear all resources {#close-extent}

Call`close()`at the very end of your session to clear all resources. If any of your test ended abruptly causing any side-affects \(not all logs sent to ExtentReports, information missing\), this method will ensure that the test is still appended to the report with a warning message.

You should call`close()`only once, at the very end \(in`@AfterSuite`for example\) as it closes the underlying stream. Once this method is called, calling any Extent method will throw an error.

Internally, this method does everything that`flush()`does by writing to the text file. Here are a few differences between`close`and`flush:`:

* If you fail to end any of your tests safely \(by calling
  `endTest`
  \),
  `close`
  will still show them in the report with a warning sign. Calling
  `Flush`
  will only write tests to the report once they are ended
* `Close`
  does not write SystemInfo to the report \(
  `flush`
  does\)
* You can call
  `flush`
  any number of times for a report session but
  `close`
  only once, because:
* Close closes the underlying stream and destroys the source references so no other Extent commands can be used

```

extent
.
Close
(
)
;
```



     Initializing Report

To initialize the report, you must create an instance of`ExtentReports`. It is possible to initialize in the following different ways:

```

var extent 
=
ExtentReports
(
string filePath
)

var extent 
=
ExtentReports
(
string filePath
,
 bool replaceExisting
)

var extent 
=
ExtentReports
(
string filePath
,
 DisplayOrder displayOrder
)

var extent 
=
ExtentReports
(
string filePath
,
 DisplayOrder displayOrder
,
 bool replaceExisting
)
```

* **filePath**
  - path of the file, in .htm or .html format
* **replaceExisting**
  - Setting to overwrite \(TRUE\) the existing file or append to it
  * True \(default\): the file will be replaced with brand new markup, and all existing data will be lost. Use this option to create a brand new report
  * False: existing data will remain, new tests will be appended to the existing report. If the the supplied path does not exist, a new file will be created.
* **displayOrder**
  * OLDEST\_FIRST \(default\) - oldest test at the top, newest at the end
  * NEWEST\_FIRST - newest test at the top, oldest at the endTo initialise thextenreports
* Initializing Report
  To initialize the report, you must create an instance of ExtentReports. It is possible to initialize in the following different ways:


  var extent = ExtentReports\(string filePath\)
  var extent = ExtentReports\(string filePath, bool replaceExisting\)
  var extent = ExtentReports\(string filePath, DisplayOrder displayOrder\)
  var extent = ExtentReports\(string filePath, DisplayOrder displayOrder, bool replaceExisting\)
  filePath - path of the file, in .htm or .html format
  replaceExisting - Setting to overwrite \(TRUE\) the existing file or append to it
  True \(default\): the file will be replaced with brand new markup, and all existing data will be lost. Use this option to create a brand new report
  False: existing data will remain, new tests will be appended to the existing report. If the the supplied path does not exist, a new file will be created.
  displayOrder
  OLDEST\_FIRST \(default\) - oldest test at the top, newest at the end
  NEWEST\_FIRST - newest test at the top, oldest at the end
* .



