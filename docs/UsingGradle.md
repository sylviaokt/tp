# Using Gradle

[Gradle](https://gradle.org/) is a build automation tool. It can automate build-related tasks such as 
* Running tests
* Managing library dependencies
* Analyzing code for style compliance

The gradle configuration for this project is defined in the _build script_  [`build.gradle`](../build.gradle). 
> The provided build script is enough for this project. <br> If you wish to modify the build script, you can 
refer [Build Scripts Basics](https://docs.gradle.org/current/userguide/tutorial_using_tasks.html) to learn
more about build scripts.

## Running Gradle Commands

To run a Gradle command, open a command window on the project folder and enter the Gradle command.
Gradle commands look like this:
* On Windows :`gradlew <task1> <task2> ...` e.g. `gradlew clean allTests`
* On Mac/Linux: `./gradlew <task1> ...`  e.g. `./gradlew clean allTests`

## Cleaning the Project

* **`clean`** <br>
  Deletes the files created during previous build tasks (e.g. files in the `build` folder).<br>
  e.g. `./gradlew clean`
  
  >**Tip `clean` to force Gradle to execute a task**: <br>
  When running a Gradle task, Gradle will try to figure out if the task needs running at all. 
  If Gradle determines that the output of the task will be same as the previous time, it will not run
  the task. For example, it will not build the JAR file again if the relevant source files have not changed
  since the last time the JAR file was built. If we want to force Gradle to run a task, we can combine
  that task with `clean`. Once the build files have been `clean`ed, Gradle has no way to determine if
  the output will be same as before, so it will be forced to execute the task.
  
## Creating the JAR file

* **`shadowJar`** <br>
  Creates the `addressbook.jar` file in the `build/jar` folder, _if the current file is outdated_.<br>
  e.g. `./gradlew shadowJar`

  > To force Gradle to create the JAR file even if the current one is up-to-date, you can '`clean`' first. <br>
    e.g. `./gradlew clean shadowJar` 

**Note: Why do we create a fat JAR?**
If we package only our own class files into the JAR file, it will not work properly unless the user has all the other
  JAR files (i.e. third party libraries) our classes depend on, which is rather inconvenient. 
  Therefore, we package all dependencies into a single JAR files, creating what is also known as a _fat_ JAR file. 
  To create a fat JAR fil, we are using the Gradle plugin [shadow jar](https://github.com/johnrengelman/shadow).

## Running Tests

* **`allTests`**<br>
  Runs all tests.

* **`guiTests`**<br>
  Runs all tests in the `guitests` package
  
* **`nonGuiTests`**<br>
  Runs all non-GUI tests in the `seedu.address` package
  
* **`headless`**<br>
  Sets the test mode as _headless_. 
  The mode is effective for that Gradle run only so it should be combined with other test tasks.
  
Here are some examples:

* `./gradlew headless allTests` -- Runs all tests in headless mode
* `./gradlew clean nonGuiTests` -- Cleans the project and runs non-GUI tests


## Updating Dependencies

There is no need to run these Gradle tasks manually as they are called automatically by other 
relevant Gradle tasks.

* **`compileJava`**<br>
 Checks whether the project has the required dependencies to compile and run the main program, and download 
 any missing dependencies before compiling the classes.<br>
 See `build.gradle` -> `allprojects` -> `dependencies` -> `compile` for the list of dependencies required.

* **`compileTestJava`**<br>
  Checks whether the project has the required dependencies to perform testing, and download 
  any missing dependencies before compiling the test classes.<br>
  See `build.gradle` -> `allprojects` -> `dependencies` -> `testCompile` for the list of 
  dependencies required.