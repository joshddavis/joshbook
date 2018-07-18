#SureFire Plugin

Plugin helps to execute all test cases under your test folder.

**Plugin Download and Docs** - http://maven.apache.org/surefire/maven-surefire-plugin/​

Select "Usage" on the site above to see how the plugin is added to the POM xml file.

​​<br/>

##### Commands

* **mvn clean** - deletes all temp files...in general its best to do this before executing...run from project folder that contains POM xml file.
* **mvn compile** - compiles code and checks for syntax errors
* **mvn test** - triggers test execution...also automatically cleans and compiles prior to executing tests...will check the .m2 repository folder looking to see if dependencies have been downloaded; if they do not exist it will connect and download the dependencies

NOTE: The word "Test" should be in the filename (classname) or it will not get executed. ie: SeleniumTest.java

​<br/>

##### TestNG Integration

In order to get mvn to follow your testng.xml for test execution, you must add the following configuration to your surefire plugin within the POM xml. Place within the <plugin> tag for surefire. NOTE: this assumes you have the testng.xml file created within the project folder.
```
<configuration>
 <suiteXmlFiles>
  <suiteXmlFile>testng.xml</suiteXmlFile>
 </suiteXmlFiles>
</configuration>
```
Additionally, you can create multiple <profiles> within the POM xml. One could be called Regression and the other could be called Smoke. Each profile has its own XML file of test cases. You can then execute the profile using the following command.
```
mvn test -PRegression
```
