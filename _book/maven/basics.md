# Maven Basics

#### Basic Terms

* **Artifact** - An artifact is a file, usually a JAR, that gets deployed to a Maven repository

* **GroupId** - GroupId will identify your project uniquely across all projects

* **archetype:generate** - Generates a new project from an archetype

<br/>

#### Creating a New Maven Project

The below line of code will create a new maven project in the current directory that will use the "quickstart" archetype. The project will be in a folder named after the artifact ID. Group ID will be the name of the initial package in the project.

```
mvn archetype:generate -DgroupId=teamsite -DartifactId=tsautomation -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

<br/>

#### Importing a Maven Project Into Eclipse

1. Before importing to eclipse, you need to make a quick change. Eclipse is expecting a .classpath file in order to import. This file does not get created using the above maven code to set up a project.
2. Navigate into the project folder that contains the POM.xml file
3. Run the following command: mvn eclipse:eclipse
4. The above command should create the .classpath file and a .project file in the working directory.
5. By default, recent versions of eclipse already contain the maven plugin. To confirm if your version of eclipse contains the plugin, go to window > preferences to see if there is a "maven" item in the left column.
6. Within that same preferences area, select "user settings" for maven. Confirm the "Local Repository" contains the path to the maven repository. It may look something like this: **"C:\Users\Josh\.m2\repository"**
7. Choose File > Import
8. Choose Maven folder and select "Existing Maven Projects" and click Next
9. The Root Directory should be set as the project folder that was created by Maven
10. Click Finish
