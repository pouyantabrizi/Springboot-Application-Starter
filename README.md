# SpringBoot-HelloWorld

Hi, I want to help you here with the simplest methods to pay attention only to the main content so that you can develop Spring Boot projects everywhere with Gradle build tools, without IDEs.
Before read this article I suggest you to read my previous simple project about create a java based project with gradle in this link: [SpringBoot-HelloWorld-Gradle](#https://github.com/pouyantabrizi/SpringBoot-HelloWorld-Gradle)

**This tutorial is a summary of the main Spring.io site tutorial and some other resources**

## Sections:
   - [What is the Spring Boot?](#one)
   - [Learn What You Can Do with Spring Boot](#two)
   - [Create project build config](#three)
   - [Create a Simple Web Application](#four)
   - [Run the Application](#five)

<h2 id="one">What You Need</h2>
About 15 minutes
- A favorite text editor or IDE
- JDK 1.8 or later
- Gradle 4+

<h2 id="two">Learn What You Can Do with Spring Boot</h2>
Spring Boot offers a fast way to build applications. It looks at your classpath and at the beans you have configured, makes reasonable assumptions about what you are missing, and adds those items. With Spring Boot, you can focus more on business features and less on infrastructure.

The following examples show what Spring Boot can do for you:

Is Spring MVC on the classpath? There are several specific beans you almost always need, and Spring Boot adds them automatically. A Spring MVC application also needs a servlet container, so Spring Boot automatically configures embedded Tomcat.

Is Jetty on the classpath? If so, you probably do NOT want Tomcat but instead want embedded Jetty. Spring Boot handles that for you.

Is Thymeleaf on the classpath? If so, there are a few beans that must always be added to your application context. Spring Boot adds them for you.

These are just a few examples of the automatic configuration Spring Boot provides. At the same time, Spring Boot does not get in your way. For example, if Thymeleaf is on your path, Spring Boot automatically adds a SpringTemplateEngine to your application context.
But if you define your own SpringTemplateEngine with your own settings, Spring Boot does not add one. This leaves you in control with little effort on your part.

<h2 id="three">Create project build config file with Gradle</h2>
The following listing shows the build.gradle file:

```
plugins {
	id 'org.springframework.boot' version '2.3.3.RELEASE'
	id 'io.spring.dependency-management' version '1.0.8.RELEASE'
	id 'java'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '1.8'

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'
	testImplementation('org.springframework.boot:spring-boot-starter-test') {
		exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
	}
}

test {
	useJUnitPlatform()
}
```

<h2 id="four">Create a Simple Web Application</h2>
Now you can create a web controller for a simple web application, as the following listing (from src/main/java/com/company/starter/HelloController.java) shows:

```java
package com.company.starter;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;

@RestController
public class HelloController {

	@RequestMapping("/")
	public String index() {
		return "Greetings from Spring Boot!";
	}

}
```

The class is flagged as a @RestController, meaning it is ready for use by Spring MVC to handle web requests. @RequestMapping maps / to the index() method. When invoked from a browser or by using curl on the command line,
the method returns pure text. That is because @RestController combines @Controller and @ResponseBody, two annotations that results in web requests returning data rather than a view.

### Create an Application class

The Spring Initializr creates a simple application class for you. However, in this case, it is too simple. You need to modify the application class to match the following listing (from src/main/java/com/example/springboot/Application.java):

```java
package com.company.starter;

import java.util.Arrays;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

}
```

@SpringBootApplication is a convenience annotation that adds all of the following:

@Configuration: Tags the class as a source of bean definitions for the application context.

@EnableAutoConfiguration: Tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings. For example, if spring-webmvc is on the classpath, this annotation flags the application as a web application and activates key behaviors, such as setting up a DispatcherServlet.

@ComponentScan: Tells Spring to look for other components, configurations, and services in the com/example package, letting it find the controllers.

The main() method uses Spring Boot’s SpringApplication.run() method to launch an application. Did you notice that there was not a single line of XML? There is no web.xml file, either. This web application is 100% pure Java and you did not have to deal with configuring any plumbing or infrastructure.


<h2 id="five">Run the Application</h2>

To run the application, run the following command in a terminal window (in the complete) directory:

./gradlew bootRun (or gradle bootRun)

now if you browse **localhost:8080** on your browser, you can see your application output.

