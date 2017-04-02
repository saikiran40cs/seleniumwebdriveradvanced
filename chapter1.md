# API Testing Using Selenium WebDriver

---

**What is API :**

An application-programming interface \(API\) is a set of programming instructions and standards for

accessing a Web-based software application or Web tool.

**Example :**

An API is a software-to-software interface, not a user interface. With APIs, applications talk to each other

without any user knowledge or intervention. When you buy movie tickets online and enter your credit

card information, the movie ticket Web site uses an API to send your credit card information to a remote

application that verifes whether your information is correct. Once payment is confirmed, the remote

application sends a response back to the movie ticket Web site saying it’s OK to issue the tickets.

**What is JSON:**

JSON \(JavaScript Object Notation\) is a lightweight, text-based, language-independent data exchange

format that is easy for humans and machines to read and write. JSON can represent two structured types:

objects and arrays. An object is an unordered collection of zero or more name/value pairs. An array is an

ordered sequence of zero or more values. The values can be strings, numbers, booleans, null, and these

two structured types.

JSON is an easier-to-use alternative to XML.

**Note : **Here i am just conferring how to parse and How to convert JsonObject to Java Object.So that you could use it your live projects using selenium.

Application contentType : Json

Objective : To validate Address : Chicago, IL, USA.

GoogleMaps API : http://maps.googleapis.com/maps/api/geocode/json?address=chicago&sensor=false

We can easily parse Json using “json-lib-2.4-jdk15.jar” Download from here…!

Please consider the below code as a reference snippet:

```
package code;

import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.Scanner;

import org.json.JSONArray;
import org.json.JSONObject;
import org.testng.Reporter;
import org.testng.annotations.Test;

public class ReadJsonObject{

@Test
public void aptTesting() throws Exception {
try {
URL url = new URL(“http://maps.googleapis.com/maps/api/geocode/json?address=chicago&sensor=false&#;);
HttpURLConnection conn = (HttpURLConnection) url.openConnection();
conn.setRequestMethod(“GET”);
conn.setRequestProperty(“Accept”, “application/json”);

if (conn.getResponseCode() != ) {
	throw new RuntimeException(” HTTP error code : ”+ conn.getResponseCode());
}

Scanner scan = new Scanner(url.openStream());
String entireResponse = new String();
while (scan.hasNext())
entireResponse += scan.nextLine();
System.out.println(“Response : “+entireResponse);
scan.close();

JSONObject obj = new JSONObject(entireResponse );
String responseCode = obj.getString(“status”);
System.out.println(“status : ” + responseCode);

JSONArray arr = obj.getJSONArray(“results”);
for (int i = 0; i < arr.length(); i++) {
String placeid = arr.getJSONObject(i).getString(“place_id”);
System.out.println(“Place id : ” + placeid);
String formatAddress = arr.getJSONObject(i).getString(“formatted_address”);
System.out.println(“Address : ” + formatAddress);

//validating Address as per the requirement
if(formatAddress.equalsIgnoreCase(“Chicago, IL, USA”))
{
System.out.println(“Address is as Expected”);
}
else
{
System.out.println(“Address is not as Expected”);
}
}
conn.disconnect();
} catch (MalformedURLException e) {
e.printStackTrace();
} catch (IOException e) {
e.printStackTrace();
}
}

```

That’s it, now you know how to convert JsonObject to Java Object and use it in your Selenium snippet.

You can practice using API : http://restcountries.eu/rest/v1



