# 🚀 Building Hybrid Framework from Scratch

## Phase 1: Project Setup

---

### Step 1.1: Create New Maven Project

**Do this in IntelliJ:**

1. **File → New → Project**
2. Select **"Maven Archetype"** (left panel)
3. Fill in:
   - **Name:** `SeleniumFramework`
   - **Location:** `D:\java\SeleniumFramework`
   - **JDK:** Select Java 17 (or your installed version)
   - **Catalog:** Maven Central
   - **Archetype:** `org.apache.maven.archetypes:maven-archetype-quickstart`
4. Click **Create**

---

### 📚 Java Concept: What is a Maven Archetype?

> An **archetype** is a project template. `maven-archetype-quickstart` creates a basic project structure with:
> - `src/main/java` - Application code
> - `src/test/java` - Test code
> - [pom.xml](cci:7://file:///D:/java/TravelEasyTests/pom.xml:0:0-0:0) - Dependencies file

---

### Step 1.2: Update pom.xml

Once project is created, **replace the entire content of [pom.xml](cci:7://file:///D:/java/TravelEasyTests/pom.xml:0:0-0:0)** with this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    
    <groupId>com.traveleasy</groupId>
    <artifactId>SeleniumFramework</artifactId>
    <version>1.0-SNAPSHOT</version>
    
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    
    <dependencies>
        <!-- Selenium WebDriver (includes Selenium Manager from 4.6+) -->
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>4.16.1</version>
        </dependency>
        
        <!-- TestNG -->
        <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>7.9.0</version>
            <scope>test</scope>
        </dependency>
        
        <!-- ExtentReports (for test reports) -->
        <dependency>
            <groupId>com.aventstack</groupId>
            <artifactId>extentreports</artifactId>
            <version>5.1.1</version>
        </dependency>
    </dependencies>
    
</project>
```

---

**After saving, click the 🔄 "Load Maven Changes" button.**

---

### 📚 Java Concept: What is each dependency for?

| Dependency | Purpose |
|------------|---------|
| `selenium-java` | Browser automation |
| `testng` | Test framework (@Test, @Before, assertions) |
| `webdrivermanager` | Auto-downloads browser drivers |
| `extentreports` | Beautiful HTML test reports |

---

### Step 1.3: Create Package Structure

In IntelliJ, create these packages:

**In `src/main/java`:**
1. Right-click `src/main/java` → New → Package → `com.traveleasy.pages`
2. Right-click `src/main/java` → New → Package → `com.traveleasy.utils`
3. Right-click `src/main/java` → New → Package → `com.traveleasy.config`

**In `src/test/java`:**
1. Right-click `src/test/java` → New → Package → `com.traveleasy.base`
2. Right-click `src/test/java` → New → Package → `com.traveleasy.tests`

**Delete any auto-generated files** like `App.java` or `AppTest.java`.

---

### Step 1.4: Create config.properties

1. Right-click `src/test/resources` → New → File → [config.properties](cci:7://file:///D:/java/TravelEasyTests/src/main/resources/config.properties:0:0-0:0)

   *(If `resources` folder doesn't exist: Right-click `src/test` → New → Directory → `resources`)*

2. Add this content:

```properties
# TravelEasy Selenium Framework Configuration

# Application URLs
base.url=http://localhost:8080
travel.url=http://localhost:8080/travel
admin.url=http://localhost:8080/admin/login

# Test Credentials
test.email=test@example.com
test.password=password123
admin.email=admin@traveleasy.com
admin.password=admin123

# Browser Settings
browser=chrome
headless=false

# Timeouts (seconds)
implicit.wait=10
explicit.wait=15
page.load.timeout=30
```

---

## ✅ Checkpoint 1

Your project structure should look like this:

```
SeleniumFramework/
├── src/
│   ├── main/
│   │   └── java/
│   │       └── com/traveleasy/
│   │           ├── pages/        ← (empty for now)
│   │           ├── utils/        ← (empty for now)
│   │           └── config/       ← (empty for now)
│   │
│   └── test/
│       ├── java/
│       │   └── com/traveleasy/
│       │       ├── base/         ← (empty for now)
│       │       └── tests/        ← (empty for now)
│       │
│       └── resources/
│           └── config.properties ← (created)
│
└── pom.xml                       ← (updated)
```

---

## 🔄 What Selenium Manager Does Automatically

1. ✅ Detects your installed browser version
2. ✅ Downloads the matching driver (chromedriver, geckodriver, etc.)
3. ✅ Caches it for future use
4. ✅ All happens behind the scenes!

---
> **Q: Do you still use WebDriverManager in your framework?**
> 
> **A:** "With Selenium 4.6+, Selenium Manager is built-in, so we don't need the external WebDriverManager dependency anymore. Selenium automatically downloads and manages browser drivers. However, for older Selenium versions or more advanced driver configuration, WebDriverManager is still useful."

---

---

## Phase 2: Create Configuration & First Test

---

### Step 2.1: Create config.properties

1. Right-click on `src/test/resources` 
2. Select **New → File**
3. Name it: [config.properties](cci:7://file:///D:/java/TravelEasyTests/src/main/resources/config.properties:0:0-0:0)
4. Add this content:

```properties
# Application URLs
base.url=http://localhost:8080
travel.url=http://localhost:8080/travel

# Test Credentials
test.email=test@example.com
test.password=password123

# Browser Settings
browser=chrome

# Timeouts (seconds)
implicit.wait=10
explicit.wait=15
```

---

### Step 2.2: Create Your First Test

1. Right-click on `src/test/java`
2. Select **New → Package** → `com.traveleasy.tests`
3. Right-click on the new `tests` package
4. Select **New → Java Class** → `FirstTest`
5. Write this code:

```java
package com.traveleasy.tests;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

public class FirstTest {
    
    // Instance variable - belongs to the object
    WebDriver driver;
    
    // Runs BEFORE each test method
    @BeforeMethod
    public void setUp() {
        // Create Chrome browser instance
        driver = new ChromeDriver();
        
        // Maximize window
        driver.manage().window().maximize();
    }
    
    // The actual test
    @Test
    public void testOpenGoogle() {
        // Navigate to Google (to verify Selenium works)
        driver.get("https://www.google.com");
        
        // Print page title
        String title = driver.getTitle();
        System.out.println("Page Title: " + title);
    }
    
    // Runs AFTER each test method
    @AfterMethod
    public void tearDown() {
        // Close browser
        if (driver != null) {
            driver.quit();
        }
    }
}
```

---

### 📚 Java Concepts in This Code

| Code | Concept | Explanation |
|------|---------|-------------|
| `WebDriver driver;` | **Instance Variable** | Declared at class level, accessible in all methods |
| `@BeforeMethod` | **Annotation** | TestNG marker - runs before each @Test |
| `driver = new ChromeDriver();` | **Object Creation** | Creates new Chrome browser object |
| `driver.get(url)` | **Method Call** | Calling a method on the driver object |
| `if (driver != null)` | **Null Check** | Prevents NullPointerException |

---

### Step 2.3: Run the Test

1. Right-click on [FirstTest.java](cci:7://file:///D:/java/TravelEasyTests/src/main/java/com/traveleasy/tests/FirstTest.java:0:0-0:0)
2. Select **Run 'FirstTest'**

---

### ✅ Expected Result

- Chrome browser opens
- Navigates to Google
- Console shows: `Page Title: Google`
- Browser closes
- Test shows **GREEN (PASSED)**



---

## Phase 3: Create BaseTest Class

**Why BaseTest?**
- Contains setup/teardown code shared by ALL tests
- Uses **inheritance** - all test classes `extend BaseTest`
- Avoids code duplication

---

### Step 3.1: Create BaseTest.java

1. Right-click on `com.traveleasy.base` (in `src/test/java`)
2. New → Java Class → `BaseTest`
3. Write this code:

```java
package com.traveleasy.base;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Optional;
import org.testng.annotations.Parameters;

import java.time.Duration;

public class BaseTest {
    
    // Protected = accessible in child classes
    protected WebDriver driver;
    
    @BeforeMethod
    @Parameters("browser")  // Can receive browser name from testng.xml
    public void setUp(@Optional("chrome") String browser) {
        
        // Create browser based on parameter
        switch (browser.toLowerCase()) {
            case "chrome":
                driver = new ChromeDriver();
                break;
            case "firefox":
                driver = new FirefoxDriver();
                break;
            case "edge":
                driver = new EdgeDriver();
                break;
            default:
                driver = new ChromeDriver();
        }
        
        // Maximize window
        driver.manage().window().maximize();
        
        // Set implicit wait
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
    }
    
    @AfterMethod
    public void tearDown() {
        if (driver != null) {
            driver.quit();
        }
    }
}
```

---

### 📚 Java Concepts in BaseTest

| Code | Concept | Explanation |
|------|---------|-------------|
| `protected WebDriver driver` | **Protected modifier** | Accessible in this class AND child classes |
| `@Parameters("browser")` | **TestNG Parameters** | Receive value from testng.xml |
| `@Optional("chrome")` | **Default value** | Use "chrome" if no parameter given |
| `switch (browser)` | **Switch statement** | Select action based on value |
| `Duration.ofSeconds(10)` | **Java Time API** | Create duration of 10 seconds |

---

### Step 3.2: Update FirstTest to Use BaseTest

Now update your [FirstTest.java](cci:7://file:///D:/java/SeleniumFramework/src/test/java/com/traveleasy/tests/FirstTest.java:0:0-0:0) to **extend BaseTest**:

```java
package com.traveleasy.tests;

import com.traveleasy.base.BaseTest;
import org.testng.annotations.Test;

public class FirstTest extends BaseTest {  // ← extends BaseTest!
    
    // No need for driver, setUp, tearDown - inherited from BaseTest!
    
    @Test
    public void testOpenGoogle() {
        driver.get("https://www.google.com");  // driver is inherited!
        String title = driver.getTitle();
        System.out.println("Page Title: " + title);
    }
    
    @Test
    public void testOpenTravelEasy() {
        driver.get("http://localhost:8080/travel");
        String title = driver.getTitle();
        System.out.println("TravelEasy Title: " + title);
    }
}
```
---

## 🎯 Java Interview Questions

### Q1: What is the difference between `public`, `private`, and `protected`?
**Expected Answer:**
> - `public`: Accessible from anywhere
> - `private`: Only within the same class
> - `protected`: Same class + child classes + same package
> - I use `protected` for the WebDriver variable so child test classes can access it through inheritance.

---

### Q2: What is inheritance? Why did you use `extends`?
**Expected Answer:**
> Inheritance allows a child class to acquire properties and methods of a parent class. I used `extends BaseTest` so that all my test classes inherit the `driver` variable and `setUp()`/`tearDown()` methods. This avoids code duplication - I write browser setup once in BaseTest, and all tests reuse it.

---

### Q3: What is the difference between `interface` and `class`?
**Expected Answer:**
> An interface defines a contract (method signatures) without implementation. A class provides the actual implementation. `WebDriver` is an interface that defines methods like [get()](cci:1://file:///D:/java/shopeasy/shopeasy/src/main/java/com/prashant/shopeasy/model/Review.java:33:4-34:37), `findElement()`. `ChromeDriver` is a class that implements these methods specifically for Chrome.

---

### Q4: What is a switch statement? When do you use it?
**Expected Answer:**
> Switch evaluates one expression against multiple possible values. I use it in BaseTest to create different browser drivers based on the browser parameter. It's cleaner than multiple if-else statements when comparing one variable against many values.

---

### Q5: What is method chaining?
**Expected Answer:**
> Method chaining is calling multiple methods in a single statement, where each method returns an object. Example: `driver.manage().window().maximize()`. Each method returns an object that has the next method, creating a fluent API.

---

### Q6: What is a null check? Why is it important?
**Expected Answer:**
> A null check verifies if an object reference is not null before using it. In `tearDown()`, I check `if (driver != null)` before calling `quit()` because if `setUp()` failed, driver would be null, and calling `null.quit()` would throw `NullPointerException`.

---

## 🎯 Selenium Interview Questions

### Q7: What is WebDriver? Is it a class or interface?
**Expected Answer:**
> WebDriver is an **interface** in Selenium that defines methods to control browsers. It's implemented by browser-specific driver classes like ChromeDriver, FirefoxDriver, and EdgeDriver. This follows the **programming to interface** principle, allowing us to switch browsers easily.

---

### Q8: What is the difference between `driver.close()` and `driver.quit()`?
**Expected Answer:**
> - [close()](cci:1://file:///D:/java/shopeasy/shopeasy/src/main/resources/templates/travel/help.html:542:8-544:9): Closes only the current browser window/tab
> - `quit()`: Closes ALL browser windows and terminates the WebDriver session completely
> 
> I always use `quit()` in `tearDown()` to ensure complete cleanup.

---

### Q9: What is implicit wait?
**Expected Answer:**
> Implicit wait tells WebDriver to wait up to a specified time when trying to find an element before throwing an exception. It's set once with `driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10))` and applies to ALL `findElement()` calls. If the element is found earlier, it continues without waiting the full time.

---

### Q10: How do you run tests on different browsers?
**Expected Answer:**
> I create a parameterized setup method using TestNG's `@Parameters` annotation. The browser name comes from testng.xml file. In the switch statement, I create the appropriate driver (ChromeDriver, FirefoxDriver, EdgeDriver) based on the parameter value.

---

## 🎯 TestNG Interview Questions

### Q11: Explain @BeforeMethod and @AfterMethod.
**Expected Answer:**
> - `@BeforeMethod`: Runs before **each** @Test method (for setup like opening browser)
> - `@AfterMethod`: Runs after **each** @Test method (for cleanup like closing browser)
> 
> If I have 5 tests, @BeforeMethod runs 5 times. This ensures each test starts with a fresh browser.

---

### Q12: What is @Optional in TestNG?
**Expected Answer:**
> `@Optional("value")` provides a default value for a parameter when it's not supplied in testng.xml. In my BaseTest, `@Optional("chrome")` means if no browser parameter is specified, Chrome is used by default.

---

### Q13: What is the execution order of TestNG annotations?
**Expected Answer:**
> ```
> @BeforeSuite → @BeforeTest → @BeforeClass → @BeforeMethod → @Test → @AfterMethod → @AfterClass → @AfterTest → @AfterSuite
> ```
> I use @BeforeMethod/@AfterMethod for browser setup/cleanup at the test method level.

---

## 🎯 Framework Design Questions

### Q14: Why do you use a BaseTest class?
**Expected Answer:**
> BaseTest serves as a parent class containing common functionality:
> 1. **Code reusability**: Setup/teardown written once
> 2. **Maintainability**: Changes in one place affect all tests
> 3. **Consistency**: All tests use the same browser configuration
> 4. **Clean tests**: Test classes focus only on test logic

---

### Q15: What design patterns are you using?
**Expected Answer:**
> - **Template Method Pattern**: BaseTest defines the skeleton (setUp/tearDown), child classes provide specific tests
> - **Page Object Model**: (Coming next) Each page has a class encapsulating elements and actions
> - **Factory Pattern**: The switch statement acts as a simple factory, creating different driver types based on input

---

