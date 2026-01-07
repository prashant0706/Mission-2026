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
---

## Phase 4: ConfigReader & Page Object Model

Now we'll create the **ConfigReader** (to read properties file) and start with **Page Objects**.

---

### Step 4.1: Create ConfigReader.java

1. Right-click on `com.traveleasy.config` (in `src/main/java`)
2. New → Java Class → `ConfigReader`
3. Write this code:

```java
package com.traveleasy.config;

import java.io.FileInputStream;
import java.io.IOException;
import java.util.Properties;

public class ConfigReader {
    
    // Properties object to hold key-value pairs
    private static Properties properties;
    
    // Static block - runs once when class is loaded
    static {
        try {
            // Load the properties file
            FileInputStream file = new FileInputStream("src/test/resources/config.properties");
            properties = new Properties();
            properties.load(file);
            file.close();
        } catch (IOException e) {
            e.printStackTrace();
            throw new RuntimeException("Could not load config.properties file!");
        }
    }
    
    // Get any property value
    public static String getProperty(String key) {
        return properties.getProperty(key);
    }
    
    // Convenience methods for common properties
    public static String getBaseUrl() {
        return properties.getProperty("base.url");
    }
    
    public static String getTravelUrl() {
        return properties.getProperty("travel.url");
    }
    
    public static String getTestEmail() {
        return properties.getProperty("test.email");
    }
    
    public static String getTestPassword() {
        return properties.getProperty("test.password");
    }
    
    public static String getBrowser() {
        return properties.getProperty("browser");
    }
    
    public static int getImplicitWait() {
        return Integer.parseInt(properties.getProperty("implicit.wait"));
    }
}
```

---

### 📚 Java Concepts in ConfigReader

| Code | Concept | Explanation |
|------|---------|-------------|
| `private static Properties` | **Static variable** | Shared by all instances, loaded once |
| `static { }` | **Static block** | Runs once when class loads |
| `FileInputStream` | **File I/O** | Reads file from disk |
| `Properties` | **Java class** | Handles key=value files |
| `getProperty(key)` | **Method call** | Gets value for a key |
| `Integer.parseInt()` | **Parsing** | Converts String to int |

---

### Step 4.2: Update BaseTest to Use ConfigReader

Update your [BaseTest.java](cci:7://file:///D:/java/SeleniumFramework/src/test/java/com/traveleasy/base/BaseTest.java:0:0-0:0) to use the config:

```java
package com.traveleasy.base;

import com.traveleasy.config.ConfigReader;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;

import java.time.Duration;

public class BaseTest {
    
    protected WebDriver driver;
    
    @BeforeMethod
    public void setUp() {
        // Get browser from config file
        String browser = ConfigReader.getBrowser();
        
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
        
        driver.manage().window().maximize();
        
        // Get timeout from config file
        int timeout = ConfigReader.getImplicitWait();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(timeout));
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

### Step 4.3: Create BasePage.java

1. Right-click on `com.traveleasy.pages` (in `src/main/java`)
2. New → Java Class → `BasePage`
3. Write this code:

```java
package com.traveleasy.pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.time.Duration;

public class BasePage {
    
    protected WebDriver driver;
    protected WebDriverWait wait;
    
    // Constructor
    public BasePage(WebDriver driver) {
        this.driver = driver;
        this.wait = new WebDriverWait(driver, Duration.ofSeconds(15));
    }
    
    // Reusable method: Click element
    protected void click(By locator) {
        wait.until(ExpectedConditions.elementToBeClickable(locator)).click();
    }
    
    // Reusable method: Type text
    protected void type(By locator, String text) {
        WebElement element = wait.until(ExpectedConditions.visibilityOfElementLocated(locator));
        element.clear();
        element.sendKeys(text);
    }
    
    // Reusable method: Get text
    protected String getText(By locator) {
        return wait.until(ExpectedConditions.visibilityOfElementLocated(locator)).getText();
    }
    
    // Reusable method: Check if element is displayed
    protected boolean isDisplayed(By locator) {
        try {
            return wait.until(ExpectedConditions.visibilityOfElementLocated(locator)).isDisplayed();
        } catch (Exception e) {
            return false;
        }
    }
    
    // Navigate to URL
    protected void navigateTo(String url) {
        driver.get(url);
    }
    
    // Get page title
    public String getPageTitle() {
        return driver.getTitle();
    }
}
```

---

### 📚 Java Concepts in BasePage

| Code | Concept | Explanation |
|------|---------|-------------|
| `public BasePage(WebDriver driver)` | **Constructor** | Initializes object with driver |
| `this.driver = driver` | **this keyword** | Refers to instance variable |
| `protected void click()` | **Protected method** | Accessible in child page classes |
| `WebDriverWait` | **Explicit wait** | Wait for specific condition |
| `ExpectedConditions` | **Wait conditions** | What to wait for |

---


## 🎯 ConfigReader - Interview Questions

### Q1: Why do you use a properties file in your framework?
**Expected Answer:**
> Properties files separate configuration from code. Benefits:
> - **No recompilation**: Change URL/credentials without rebuilding
> - **Environment flexibility**: Different configs for dev, staging, production
> - **Security**: Credentials not hardcoded in source code
> - **Maintainability**: Easy to update by anyone

---

### Q2: What is a static block in Java? Why did you use it in ConfigReader?
**Expected Answer:**
> A static block runs **once** when the class is first loaded into memory, before any method calls. I use it in ConfigReader to:
> - Load the properties file only once
> - Make the Properties object available immediately
> - Avoid repeated file reading
> ```java
> static {
>     // This runs once when ConfigReader is first used
>     properties = new Properties();
>     properties.load(new FileInputStream("config.properties"));
> }
> ```

---

### Q3: What is the difference between static and instance variables?
**Expected Answer:**
> | Static Variable | Instance Variable |
> |----------------|-------------------|
> | Belongs to the **class** | Belongs to **object** |
> | Shared by all objects | Each object has its own copy |
> | One copy in memory | Multiple copies possible |
> | Access: `ClassName.variable` | Access: `object.variable` |
> 
> I use `static Properties` in ConfigReader because config should be loaded once and shared across all tests.

---

### Q4: How do you read a properties file in Java?
**Expected Answer:**
> ```java
> Properties properties = new Properties();
> FileInputStream file = new FileInputStream("path/to/file.properties");
> properties.load(file);
> String value = properties.getProperty("key");
> file.close();
> ```
> The Properties class handles key=value format files automatically.

---

### Q5: What exception handling did you use in ConfigReader?
**Expected Answer:**
> I used try-catch to handle `IOException` which can occur if:
> - File doesn't exist
> - File path is wrong
> - File is not readable
> 
> I throw a `RuntimeException` with a clear message so tests fail fast with meaningful error.

---

## 🎯 BasePage - Interview Questions

### Q6: What is Page Object Model (POM)?
**Expected Answer:**
> POM is a design pattern where each web page has a corresponding Java class containing:
> - **Locators** (private)
> - **Page actions as methods** (public)
> 
> Benefits:
> - **Reusability**: Page methods used by multiple tests
> - **Maintainability**: UI change = update one class
> - **Readability**: Tests read like user actions
> - **Separation of concerns**: Tests focus on logic, pages handle elements

---

### Q7: Why do you have a BasePage class?
**Expected Answer:**
> BasePage is a parent class containing common functionality used by all page classes:
> - Driver and wait initialization
> - Common methods: [click()](cci:1://file:///D:/java/shopeasy/shopeasy/src/main/resources/templates/travel/seat-selection.html:377:24-377:64), `type()`, `getText()`
> - Page navigation methods
> 
> All specific pages (LoginPage, HomePage) extend BasePage and inherit these methods.

---

### Q8: What is the difference between implicit wait and explicit wait?
**Expected Answer:**
> | Implicit Wait | Explicit Wait |
> |---------------|---------------|
> | Set once, applies to ALL findElement() | Set for specific element/condition |
> | `driver.manage().timeouts().implicitlyWait()` | `WebDriverWait` + `ExpectedConditions` |
> | Waits for element presence | Waits for specific condition |
> | Less flexible | More precise control |
> 
> I use **explicit waits** in BasePage methods because different elements need different conditions (clickable, visible, etc.).

---

### Q9: What is ExpectedConditions? Give examples.
**Expected Answer:**
> `ExpectedConditions` provides ready-made conditions for WebDriverWait:
> ```java
> ExpectedConditions.visibilityOfElementLocated(locator)  // Element is visible
> ExpectedConditions.elementToBeClickable(locator)        // Element can be clicked
> ExpectedConditions.presenceOfElementLocated(locator)    // Element exists in DOM
> ExpectedConditions.invisibilityOfElementLocated(locator) // Element disappears
> ExpectedConditions.textToBePresentInElement(element, "text") // Text appears
> ExpectedConditions.alertIsPresent()                      // Alert popup
> ```

---

### Q10: What is a constructor? Why does BasePage have one?
**Expected Answer:**
> A constructor is a special method called when creating an object. It initializes the object's state.
> ```java
> public BasePage(WebDriver driver) {
>     this.driver = driver;
>     this.wait = new WebDriverWait(driver, Duration.ofSeconds(15));
> }
> ```
> BasePage constructor receives the WebDriver and initializes the wait object. Child pages pass the driver when calling `super(driver)`.

---

### Q11: Explain the `this` keyword.
**Expected Answer:**
> `this` refers to the current object instance. Used to:
> - Distinguish instance variable from parameter with same name
> - Call another constructor in same class
> - Pass current object as parameter
> 
> ```java
> public BasePage(WebDriver driver) {
>     this.driver = driver;  // this.driver = instance variable
>                            // driver = parameter
> }
> ```

---

### Q12: How does your click() method work?
**Expected Answer:**
> ```java
> protected void click(By locator) {
>     wait.until(ExpectedConditions.elementToBeClickable(locator)).click();
> }
> ```
> 1. Wait until element is clickable (visible + enabled)
> 2. Return the element
> 3. Click on it
> 
> This prevents `ElementNotClickable` and `StaleElement` exceptions.

---

### Q13: What is method chaining in your BasePage?
**Expected Answer:**
> Method chaining calls multiple methods in one statement:
> ```java
> wait.until(ExpectedConditions.elementToBeClickable(locator)).click();
> ```
> - `wait.until()` returns WebElement
> - `.click()` is called on that WebElement
> 
> This is more concise than storing in a variable first.

---

## 🎯 Design Pattern Questions

### Q14: What design patterns are you using in your framework?
**Expected Answer:**
> 1. **Page Object Model**: Encapsulates page elements and actions
> 2. **Template Method**: BaseTest/BasePage define skeleton, child classes add specifics
> 3. **Singleton (partial)**: ConfigReader loads properties once (static)
> 4. **Factory**: BaseTest creates different drivers based on config

---

### Q15: How do child page classes use BasePage?
**Expected Answer:**
> ```java
> public class LoginPage extends BasePage {
>     
>     public LoginPage(WebDriver driver) {
>         super(driver);  // Call BasePage constructor
>     }
>     
>     private By emailField = By.id("email");
>     
>     public void enterEmail(String email) {
>         type(emailField, email);  // Use inherited method
>     }
> }
> ```
> The child:
> - Extends BasePage
> - Calls `super(driver)` to initialize parent
> - Uses inherited methods like `type()`, [click()](cci:1://file:///D:/java/shopeasy/shopeasy/src/main/resources/templates/travel/seat-selection.html:377:24-377:64)

---

## 📊 Quick Reference Card

| Concept | Key Point |
|---------|-----------|
| Static block | Runs once when class loads |
| Static variable | Shared across all instances |
| Properties | Reads key=value files |
| Constructor | Initializes object state |
| `this` keyword | Refers to current object |
| Implicit wait | Global, for all elements |
| Explicit wait | Specific element + condition |
| ExpectedConditions | Predefined wait conditions |
| BasePage | Parent with common methods |
| Page Object Model | Page = Class pattern |

---



## 🚀 Phase 5: Create Your First Page Object (LoginPage)

Now we'll create a real page object for TravelEasy's login page!

---

### Step 5.1: Create LoginPage.java

1. Right-click on `com.traveleasy.pages` (in `src/main/java`)
2. New → Java Class → `LoginPage`
3. Write this code:

```java
package com.traveleasy.pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class LoginPage extends BasePage {
    
    // Locators - using data-testid attributes from TravelEasy
    private By emailInput = By.cssSelector("[data-testid='email-input']");
    private By passwordInput = By.cssSelector("[data-testid='password-input']");
    private By loginButton = By.cssSelector("[data-testid='login-button']");
    private By errorMessage = By.cssSelector("[data-testid='error-message']");
    private By registerLink = By.linkText("Register here");
    
    // Constructor
    public LoginPage(WebDriver driver) {
        super(driver);  // Call BasePage constructor
    }
    
    // Navigate to login page
    public LoginPage open(String url) {
        navigateTo(url + "/login");
        return this;
    }
    
    // Enter email
    public LoginPage enterEmail(String email) {
        type(emailInput, email);
        return this;
    }
    
    // Enter password
    public LoginPage enterPassword(String password) {
        type(passwordInput, password);
        return this;
    }
    
    // Click login button
    public HomePage clickLogin() {
        click(loginButton);
        return new HomePage(driver);  // Return next page
    }
    
    // Combined login method
    public HomePage login(String email, String password) {
        enterEmail(email);
        enterPassword(password);
        return clickLogin();
    }
    
    // Get error message
    public String getErrorMessage() {
        return getText(errorMessage);
    }
    
    // Check if error is displayed
    public boolean isErrorDisplayed() {
        return isDisplayed(errorMessage);
    }
    
    // Click register link
    public void clickRegister() {
        click(registerLink);
    }
}
```

---

### 📚 Key Concepts in LoginPage

| Code | Concept | Explanation |
|------|---------|-------------|
| `extends BasePage` | **Inheritance** | Gets driver, wait, common methods |
| `super(driver)` | **Super constructor** | Calls parent's constructor |
| `return this` | **Method chaining** | Allows `page.enterEmail().enterPassword()` |
| `return new HomePage(driver)` | **Page transition** | Returns next page after action |
| `By.cssSelector("[data-testid='x']")` | **Locator strategy** | Uses data-testid for stability |

---

### Step 5.2: Create HomePage.java

1. Right-click on `com.traveleasy.pages` (in `src/main/java`)
2. New → Java Class → `HomePage`
3. Write this code:

```java
package com.traveleasy.pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class HomePage extends BasePage {
    
    // Locators
    private By welcomeMessage = By.cssSelector("[data-testid='welcome-message']");
    private By logoutButton = By.cssSelector("[data-testid='logout-button']");
    private By flightsLink = By.linkText("Flights");
    private By busesLink = By.linkText("Buses");
    
    // Constructor
    public HomePage(WebDriver driver) {
        super(driver);
    }
    
    // Check if user is logged in (welcome message visible)
    public boolean isLoggedIn() {
        return isDisplayed(welcomeMessage);
    }
    
    // Get welcome message text
    public String getWelcomeMessage() {
        return getText(welcomeMessage);
    }
    
    // Click logout
    public LoginPage logout() {
        click(logoutButton);
        return new LoginPage(driver);
    }
    
    // Navigate to flights
    public void goToFlights() {
        click(flightsLink);
    }
    
    // Navigate to buses
    public void goToBuses() {
        click(busesLink);
    }
}
```

---

### Step 5.3: Create LoginTest.java

1. Right-click on `com.traveleasy.tests` (in `src/test/java`)
2. New → Java Class → `LoginTest`
3. Write this code:

```java
package com.traveleasy.tests;

import com.traveleasy.base.BaseTest;
import com.traveleasy.config.ConfigReader;
import com.traveleasy.pages.HomePage;
import com.traveleasy.pages.LoginPage;
import org.testng.Assert;
import org.testng.annotations.Test;

public class LoginTest extends BaseTest {
    
    @Test
    public void testValidLogin() {
        // Arrange
        LoginPage loginPage = new LoginPage(driver);
        String baseUrl = ConfigReader.getBaseUrl();
        
        // Act
        loginPage.open(baseUrl);
        HomePage homePage = loginPage.login(
            ConfigReader.getTestEmail(),
            ConfigReader.getTestPassword()
        );
        
        // Assert
        Assert.assertTrue(homePage.isLoggedIn(), "User should be logged in");
    }
    
    @Test
    public void testInvalidLogin() {
        // Arrange
        LoginPage loginPage = new LoginPage(driver);
        String baseUrl = ConfigReader.getBaseUrl();
        
        // Act
        loginPage.open(baseUrl);
        loginPage.enterEmail("wrong@email.com");
        loginPage.enterPassword("wrongpassword");
        loginPage.clickLogin();
        
        // Assert
        Assert.assertTrue(loginPage.isErrorDisplayed(), "Error message should be displayed");
    }
    
    @Test
    public void testLoginPageTitle() {
        // Arrange
        LoginPage loginPage = new LoginPage(driver);
        
        // Act
        loginPage.open(ConfigReader.getBaseUrl());
        String title = loginPage.getPageTitle();
        
        // Assert
        System.out.println("Page Title: " + title);
        Assert.assertNotNull(title, "Page title should not be null");
    }
}
```

---

### 📚 Key Concepts in LoginTest

| Code | Concept | Explanation |
|------|---------|-------------|
| `extends BaseTest` | **Inheritance** | Gets driver, setUp, tearDown |
| `Assert.assertTrue()` | **TestNG Assertion** | Verifies condition is true |
| `Assert.assertNotNull()` | **Null assertion** | Verifies object is not null |
| `// Arrange, Act, Assert` | **AAA Pattern** | Test structure best practice |

---

## 🎯 Your Tasks

1. ✅ Create `LoginPage.java` in `com.traveleasy.pages`
2. ✅ Create `HomePage.java` in `com.traveleasy.pages`
3. ✅ Create `LoginTest.java` in `com.traveleasy.tests`
4. ⚠️ **Start TravelEasy app first** before running tests!
5. ✅ Run `LoginTest`

## Q1: "What is ChromeOptions in Selenium?"

> **Answer:** "ChromeOptions is a class in Selenium that allows us to customize Chrome browser behavior before launching it. We can set arguments like headless mode, disable notifications, set download paths, handle SSL certificates, enable/disable features, and configure browser preferences.
>
> For example:
> ```java
> ChromeOptions options = new ChromeOptions();
> options.addArguments("--headless");           // Run without UI
> options.addArguments("--disable-notifications"); // Block popups
> driver = new ChromeDriver(options);
> ```
>
> It's essential for CI/CD pipelines where we run tests in headless mode, and for handling real-world scenarios like cookies, SSL, and downloads."

---

## Q2: "Can you share a real scenario where you used ChromeOptions?"

> **Answer:** "Yes! In my project, after a successful login, the application was redirecting to a URL with `jsessionid` appended, like `http://localhost:8080/;jsessionid=XYZ`. This caused a 404 error.
>
> When I tested manually, it worked fine. After debugging, I realized that Selenium's Chrome browser wasn't accepting cookies properly, so the application fell back to **URL-based session tracking** instead of **cookie-based session tracking**.
>
> I fixed it by adding ChromeOptions:
> ```java
> ChromeOptions options = new ChromeOptions();
> options.addArguments("--disable-blink-features=AutomationControlled");
> driver = new ChromeDriver(options);
> ```
>
> This made the browser behave more like a regular user's browser, and cookies worked correctly."

---

## Q3: "What is the difference between cookie-based and URL-based sessions?"

> **Answer:**
>
> | Cookie-Based Session | URL-Based Session |
> |---------------------|-------------------|
> | Session ID stored in browser cookie | Session ID appended to URL |
> | `Cookie: JSESSIONID=ABC123` | `/page;jsessionid=ABC123` |
> | More secure | Less secure (URL can be shared/logged) |
> | Used when cookies are enabled | Fallback when cookies are blocked |
>
> Selenium sometimes blocks cookies by default, so servers use URL-rewriting as a fallback. That's why we configure ChromeOptions to enable proper cookie handling."

---

## Q4: "What are common ChromeOptions you've used?"

> **Answer:** "Here are the most common ones I use:
>
> ```java
> ChromeOptions options = new ChromeOptions();
> 
> // 1. Headless mode (for CI/CD)
> options.addArguments("--headless");
> 
> // 2. Disable notifications
> options.addArguments("--disable-notifications");
> 
> // 3. Maximize window
> options.addArguments("--start-maximized");
> 
> // 4. Disable 'Chrome is being controlled' banner
> options.addArguments("--disable-blink-features=AutomationControlled");
> 
> // 5. Incognito mode
> options.addArguments("--incognito");
> 
> // 6. Disable GPU (for Linux servers)
> options.addArguments("--disable-gpu");
> 
> // 7. Accept insecure certificates
> options.setAcceptInsecureCerts(true);
> ```"

---

## Q5: "What does `--disable-blink-features=AutomationControlled` do?"

> **Answer:** "This option removes the automation-detection features that Chrome uses to identify automated browsers. Many websites detect Selenium tests by checking the `navigator.webdriver` property which is set to `true` when Chrome runs in automation mode.
>
> By disabling this feature:
> - The browser appears more like a regular user's browser
> - Some websites won't block or behave differently with your tests
> - Cookies and sessions work more naturally
>
> It's especially useful when testing applications that have bot-detection mechanisms."

---
Q: What is the difference between cookie-based and URL-based session tracking?

A: "Both are ways to maintain user sessions since HTTP is stateless.

Cookie-based stores the session ID in a browser cookie (JSESSIONID). It's more secure because the session ID is sent in HTTP headers, not visible in the URL, and can't be accidentally shared.

URL-based appends the session ID to every URL like /page;jsessionid=ABC123. It's a fallback used when cookies are blocked. It's less secure because the session can be shared through copied URLs.

I encountered this issue when my Selenium tests failed after login - the browser was blocking cookies, so the app used URL-based sessions which created malformed URLs. I fixed it by configuring ChromeOptions to make the browser behave like a normal user's browser."



## 📝 Summary for Interview

| Concept | Key Points |
|---------|------------|
| **ChromeOptions** | Customize Chrome before launching |
| **Headless** | `--headless` for CI/CD |
| **Session Issue** | jsessionid in URL = cookies blocked |
| **Fix** | Use ChromeOptions to enable proper cookie handling |
| **Real Example** | Login redirect failing due to URL-based sessions |


# Phase 6: Advanced Features - Exact Conversation Notes

---

# Step 1: XPath Explained

## What is XPath?
XPath = **XML Path Language**. It's used to navigate through HTML elements to find them.

## XPath Syntax Basics

### Absolute XPath (❌ Avoid)
```
/html/body/div[1]/div[2]/form/input[1]
```

### Relative XPath (✅ Use This!)
```
//input[@id='email']
```

## Basic Syntax
```
//tagname[@attribute='value']
```

| Part | Meaning |
|------|---------|
| `//` | Search anywhere in document |
| `tagname` | HTML tag (input, button, div) |
| `@attribute` | Attribute name (id, class, name) |
| `'value'` | Attribute value |

## Common Examples
| What You Want | XPath |
|---------------|-------|
| Input by ID | `//input[@id='email']` |
| Button by class | `//button[@class='btn-login']` |
| Link by text | `//a[text()='Login']` |
| Contains (partial) | `//div[contains(@class, 'product')]` |

## Using in Selenium
```java
By.xpath("//input[@id='email']")
By.cssSelector(".product-card")
```

---

# Step 2: Create ProductsPage.java

## Location
`D:\java\SeleniumFramework\src\main\java\com\traveleasy\pages\ProductsPage.java`

## Locators for ProductsPage (based on actual HTML)
| Element | Locator |
|---------|---------|
| Product cards | `By.cssSelector(".product-card")` |
| Product title | `By.xpath("//div[@class='product-info']/h3")` |
| Add to Cart | `By.cssSelector(".add-to-cart")` |

## Template 
```java
package com.traveleasy.pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class ProductsPage extends BasePage {

    // TODO: Add locators
    // Hint: Check http://localhost:8080/products for element IDs/classes
    // You need locators for:
    // - Product cards (class="product-card")
    // - Product title (class="product-title" or similar)
    // - Add to Cart button
    // - Category filter links

    // Constructor - call super(driver)
    public ProductsPage(WebDriver driver) {
        // TODO: Call parent constructor
    }

    // Open products page
    public ProductsPage open(String baseUrl) {
        // TODO: Navigate to baseUrl + "/products"
        return this;
    }

    // Check if products are displayed
    public boolean areProductsDisplayed() {
        // TODO: Return true if product cards are visible
        return false;
    }

    // Click on first product
    public void clickFirstProduct() {
        // TODO: Click the first product card
    }

    // Add product to cart
    public ProductsPage addToCart() {
        // TODO: Click add to cart button
        return this;
    }
}
```

## Code Review Feedback I Gave:
- Variable names should be **lowercase** (`productCard` not `ProductCard`)
- Add `private` to locators
- Remove unused imports

---

# Step 3: Create CartPage.java

## Location
`D:\java\SeleniumFramework\src\main\java\com\traveleasy\pages\CartPage.java`

## Locators for CartPage
| Element | Locator |
|---------|---------|
| Empty cart div | `By.cssSelector(".cart-empty")` |
| Cart items | `By.cssSelector(".cart-item")` |
| Checkout button | `By.cssSelector(".checkout-btn")` |

## Template 
```java
package com.traveleasy.pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class CartPage extends BasePage {
    
    // TODO: Add locators here
    
    // Constructor
    public CartPage(WebDriver driver) {
        // TODO
    }
    
    // Open cart page
    public CartPage open(String baseUrl) {
        // TODO: Navigate to baseUrl + "/cart"
    }
    
    // Check if cart is empty
    public boolean isCartEmpty() {
        // TODO: Return true if empty cart div is displayed
    }
    
    // Check if cart has items
    public boolean hasItems() {
        // TODO: Return true if cart items are displayed
    }
    
    // Get item count
    public int getItemCount() {
        // TODO: Return number of items (hint: use findElements and .size())
    }
    
    // Click checkout
    public void clickCheckout() {
        // TODO: Click checkout button
    }
}
```

## Bug to ignore
```java
// WRONG - XPath syntax in cssSelector!
By.cssSelector("//h2[text()='Your cart is empty!']")

// CORRECT - Use xpath() for XPath syntax
By.xpath("//h2[text()='Your cart is empty!']")
```

---

# Step 4: Create ProductsTest.java

## Template
```java
package com.traveleasy.tests;

import com.traveleasy.base.BaseTest;
import com.traveleasy.config.ConfigReader;
import com.traveleasy.pages.ProductsPage;
import org.testng.Assert;
import org.testng.annotations.Test;

public class ProductsTest extends BaseTest {

    @Test
    public void testProductsPageDisplaysProducts() {
        // TODO: Create ProductsPage, open it, verify products are displayed
    }

    @Test
    public void testClickFirstProduct() {
        // TODO: Click first product and verify navigation
    }
}
```

## My Review Feedback:
Your tests were missing **assertions**! Without assertions, the test will always "pass".

```java
// Wrong - no assertion
productPage.areProductsDisplayed();

// Correct - with assertion
Assert.assertTrue(productPage.areProductsDisplayed(), 
    "Products should be displayed on the page");
```

---

# Q&A: Does Assertion Show Message on Success?

**Your Question:** Does assertion give any message when succeeded?

**My Answer:** **No!** Assertions are **silent on success**. They only speak when they fail.

```java
Assert.assertTrue(condition, "Error message if fails");
```

| Condition | What Happens |
|-----------|--------------|
| `true` (Pass) | Nothing! Silent. Test continues. ✅ |
| `false` (Fail) | Throws `AssertionError` with your message ❌ |

If you want success messages:
```java
Assert.assertTrue(displayed, "Products should be displayed");
System.out.println("✅ Test passed: Products are displayed!");
```

---

# Step 5: Create CartTest.java

## Template
```java
package com.traveleasy.tests;

import com.traveleasy.base.BaseTest;
import com.traveleasy.config.ConfigReader;
import com.traveleasy.pages.CartPage;
import com.traveleasy.pages.ProductsPage;
import org.testng.Assert;
import org.testng.annotations.Test;

public class CartTest extends BaseTest {

    @Test
    public void testEmptyCart() {
        // Open cart page directly
        // Assert that cart is empty
    }

    @Test
    public void testAddItemToCart() {
        // 1. Open products page
        // 2. Add a product to cart
        // 3. Open cart page
        // 4. Assert cart has items
    }
}
```

---

# Step 6: Data-Driven Testing (DataProvider)

## What is DataProvider?
Runs the same test multiple times with different data.

## How It Works - Visual
```
DataProvider Array:
┌─────────────────────────────────────────────────────┐
│ Row 0: ["test@example.com", "password123", true]    │
│ Row 1: ["wrong@email.com", "wrongpass", false]      │
│ Row 2: ["", "password123", false]                   │
│ Row 3: ["test@example.com", "", false]              │
└─────────────────────────────────────────────────────┘
                    │
                    ▼
Test runs 4 times:
  Run 1: email="test@example.com", shouldPass=true
  Run 2: email="wrong@email.com", shouldPass=false
  Run 3: email="", shouldPass=false
  Run 4: email="test@example.com", password="", shouldPass=false
```

## Code  to Add to LoginTest.java
```java
@DataProvider(name = "loginData")
public Object[][] getLoginData() {
    return new Object[][] {
        {"test@example.com", "password123", true},   // Valid login
        {"wrong@email.com", "wrongpass", false},     // Invalid login
        {"", "password123", false},                   // Empty email
        {"test@example.com", "", false}              // Empty password
    };
}

@Test(dataProvider = "loginData")
public void testLoginWithMultipleData(String email, String password, boolean shouldPass) {
    LoginPage loginPage = new LoginPage(driver);
    loginPage.open(ConfigReader.getBaseUrl());
    loginPage.enterEmail(email);
    loginPage.enterPassword(password);
    
    if (shouldPass) {
        loginPage.clickLogin();
        HomePage homePage = new HomePage(driver);
        Assert.assertTrue(homePage.isLoggedIn(), "Login should succeed");
    } else {
        loginPage.clickLoginExpectingError();
        Assert.assertTrue(loginPage.isErrorDisplayed(), "Error should show");
    }
}
```

## Import to Add
```java
import org.testng.annotations.DataProvider;
```


# Q&A: HTML5 Form Validation

** Question:** For empty email/password, the website asks to provide the field instead of showing error.

** Answer:** That's **HTML5 form validation** (browser-level). When email/password is empty, the browser shows its own validation popup:
```
"Please fill in this field"
```

This happens **before** the form is submitted, so:
- The form never reaches the server
- No custom error message from the app
- Our assertion `isErrorDisplayed()` fails!

**Fix:** Update DataProvider to only 2 rows:
```java
@DataProvider(name = "loginData")
public Object[][] getLoginData() {
    return new Object[][] {
        {"test@example.com", "password123", true},   // Valid login
        {"wrong@email.com", "wrongpass", false}      // Invalid login
    };
}
```

---

# Step 7: ExtentReports Integration

## Step 7.1: Create ExtentReportManager.java

**Location:** `D:\java\SeleniumFramework\src\main\java\com\traveleasy\utils\ExtentReportManager.java`

## Complete Code 
```java
package com.traveleasy.utils;

import com.aventstack.extentreports.ExtentReports;
import com.aventstack.extentreports.ExtentTest;
import com.aventstack.extentreports.reporter.ExtentSparkReporter;

public class ExtentReportManager {
    private static ExtentReports extent;
    private static ExtentTest test;

    public static ExtentReports getInstance() {
        if (extent == null) {
            ExtentSparkReporter spark = new ExtentSparkReporter("test-output/ExtentReport.html");
            spark.config().setDocumentTitle("ShopEasy Test Report");
            spark.config().setReportName("Automation Test Results");
            
            extent = new ExtentReports();
            extent.attachReporter(spark);
            extent.setSystemInfo("Tester", "Prashant Rathod");
            extent.setSystemInfo("Environment", "QA");
        }
        return extent;
    }

    public static ExtentTest createTest(String testName) {
        test = getInstance().createTest(testName);
        return test;
    }

    public static void flush() {
        if (extent != null) {
            extent.flush();
        }
    }
}
```

## Step 7.2: Update BaseTest.java

## Complete Updated BaseTest.java Code
```java
package com.traveleasy.base;

import com.traveleasy.config.ConfigReader;
import com.traveleasy.utils.ExtentReportManager;
import com.aventstack.extentreports.ExtentTest;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.ITestResult;
import org.testng.annotations.*;

import java.time.Duration;

public class BaseTest {
    protected WebDriver driver;
    protected ExtentTest extentTest;

    @BeforeMethod
    public void setUp(ITestResult result) {
        // Create ExtentTest for this test method
        extentTest = ExtentReportManager.createTest(result.getMethod().getMethodName());
        
        String browser = ConfigReader.getBrowser();
        switch (browser.toLowerCase()) {
            case "chrome":
                ChromeOptions options = new ChromeOptions();
                options.addArguments("--disable-blink-features=AutomationControlled");
                driver = new ChromeDriver(options);
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

        driver.manage().window().maximize();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
    }

    @AfterMethod
    public void tearDown(ITestResult result) {
        // Log test result to ExtentReports
        if (result.getStatus() == ITestResult.FAILURE) {
            extentTest.fail("Test Failed: " + result.getThrowable().getMessage());
        } else if (result.getStatus() == ITestResult.SUCCESS) {
            extentTest.pass("Test Passed");
        } else {
            extentTest.skip("Test Skipped");
        }
        
        if (driver != null) {
            driver.quit();
        }
    }

    @AfterSuite
    public void tearDownSuite() {
        ExtentReportManager.flush();  // Generate the report!
    }
}
```

## Key Changes Explained:
1. Added `ITestResult result` parameter to get test name
2. Created `extentTest` for each test
3. Log pass/fail/skip in `@AfterMethod`
4. `flush()` in `@AfterSuite` to generate the HTML report

## After Running Tests
Open: `test-output/ExtentReport.html`

---

# ExtentReports Explained

## What is ExtentReports?
Creates beautiful HTML test reports instead of console output.

## Three Key Components
| Component | Purpose |
|-----------|---------|
| ExtentReports | Main engine that collects test data |
| ExtentSparkReporter | Converts data to HTML format |
| ExtentTest | Represents one test case |

## Architecture
```
Tests Run → ExtentReportManager → ExtentSparkReporter → HTML Report
```

## Key Points
- `flush()` MUST be called to generate the HTML file
- Report saved at `test-output/ExtentReport.html`

---

# Interview Questions

## Q: How do you write XPath?
"I use the syntax `//tagname[@attribute='value']`. For partial matches, I use `contains()`. For example, `//div[contains(@class, 'product')]`."

## Q: What is DataProvider in TestNG?
"DataProvider allows running the same test with different data sets. It returns a 2D Object array where each row is one test execution."

## Q: What is ExtentReports?
"ExtentReports generates HTML test reports with dashboards and pass/fail charts. I integrate it with TestNG's BeforeMethod and AfterMethod. Must call flush() at end to generate the file."


# Phase 7: Complete Code Changes Tutorial

This document contains all the complete file changes made during Phase 7.
Follow these steps in order to implement all features.

---

# File 1: ScreenshotUtil.java (NEW FILE)

**Location:** `src/main/java/com/traveleasy/utils/ScreenshotUtil.java`

**Create this complete file:**

```java
package com.traveleasy.utils;

import com.traveleasy.pages.BasePage;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.StandardCopyOption;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Base64;
import java.util.Date;
import java.util.List;

public class ScreenshotUtil {

    // Take screenshot and return as Base64 (for embedding in report)
    public static String takeScreenshotAsBase64(WebDriver driver) {
        TakesScreenshot ts = (TakesScreenshot) driver;
        return ts.getScreenshotAs(OutputType.BASE64);
    }

    // Take screenshot at failure point and save to file
    public static String takeScreenshot(WebDriver driver, String testName) {
        File screenshotDir = new File("screenshots");
        if (!screenshotDir.exists()) {
            screenshotDir.mkdirs();
        }

        String timestamp = new SimpleDateFormat("yyyy-MM-dd_HH-mm-ss").format(new Date());
        String fileName = testName + "_FAILURE_" + timestamp + ".png";

        TakesScreenshot ts = (TakesScreenshot) driver;
        File source = ts.getScreenshotAs(OutputType.FILE);
        File destination = new File(screenshotDir, fileName);

        try {
            Files.copy(source.toPath(), destination.toPath(), StandardCopyOption.REPLACE_EXISTING);
            System.out.println("Failure screenshot saved: " + destination.getAbsolutePath());
        } catch (IOException e) {
            System.out.println("Failed to save screenshot: " + e.getMessage());
        }

        return destination.getAbsolutePath();
    }

    // Save all step screenshots (only call on failure)
    public static List<StepScreenshotData> saveStepScreenshots(String testName) {
        List<StepScreenshotData> savedData = new ArrayList<>();
        
        File screenshotDir = new File("screenshots/" + testName);
        if (!screenshotDir.exists()) {
            screenshotDir.mkdirs();
        }

        String timestamp = new SimpleDateFormat("yyyy-MM-dd_HH-mm-ss").format(new Date());
        
        int stepNumber = 1;
        for (BasePage.StepScreenshot step : BasePage.stepScreenshots) {
            String fileName = String.format("Step_%02d_%s.png", stepNumber, timestamp);
            File destination = new File(screenshotDir, fileName);
            
            try {
                Files.copy(step.screenshot.toPath(), destination.toPath(), StandardCopyOption.REPLACE_EXISTING);
                
                // Read file as Base64 for embedding in report
                byte[] fileContent = Files.readAllBytes(destination.toPath());
                String base64 = Base64.getEncoder().encodeToString(fileContent);
                
                savedData.add(new StepScreenshotData(stepNumber, step.description, base64, destination.getAbsolutePath()));
                System.out.println("Step " + stepNumber + " saved: " + step.description);
            } catch (IOException e) {
                System.out.println("Failed to save step screenshot: " + e.getMessage());
            }
            stepNumber++;
        }
        
        System.out.println("Total " + savedData.size() + " step screenshots saved");
        return savedData;
    }

    // Data class to hold step screenshot info
    public static class StepScreenshotData {
        public int stepNumber;
        public String description;
        public String base64Image;
        public String filePath;

        public StepScreenshotData(int stepNumber, String description, String base64Image, String filePath) {
            this.stepNumber = stepNumber;
            this.description = description;
            this.base64Image = base64Image;
            this.filePath = filePath;
        }
    }
}
```

---

# File 2: BasePage.java (UPDATED)

**Location:** `src/main/java/com/traveleasy/pages/BasePage.java`

**Replace entire file with:**

```java
package com.traveleasy.pages;

import org.openqa.selenium.By;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.io.File;
import java.time.Duration;
import java.util.ArrayList;
import java.util.List;

public class BasePage {

    protected WebDriver driver;
    protected WebDriverWait wait;
    
    // Store step screenshots in memory (only saved if test fails)
    public static List<StepScreenshot> stepScreenshots = new ArrayList<>();

    // Inner class to store screenshot with description
    public static class StepScreenshot {
        public File screenshot;
        public String description;
        
        public StepScreenshot(File screenshot, String description) {
            this.screenshot = screenshot;
            this.description = description;
        }
    }

    public BasePage(WebDriver driver) {
        this.driver = driver;
        this.wait = new WebDriverWait(driver, Duration.ofSeconds(15));
    }

    // Capture screenshot at current step
    private void captureStepScreenshot(String action) {
        try {
            TakesScreenshot ts = (TakesScreenshot) driver;
            File screenshot = ts.getScreenshotAs(OutputType.FILE);
            stepScreenshots.add(new StepScreenshot(screenshot, action));
        } catch (Exception e) {
            System.out.println("Could not capture step screenshot: " + e.getMessage());
        }
    }

    // Clear screenshots (call before each test)
    public static void clearStepScreenshots() {
        stepScreenshots.clear();
    }

    protected void click(By locator) {
        wait.until(ExpectedConditions.visibilityOfElementLocated(locator)).click();
        captureStepScreenshot("Click on: " + locator.toString());
    }

    protected void type(By locator, String text) {
        WebElement element = wait.until(ExpectedConditions.visibilityOfElementLocated(locator));
        element.clear();
        element.sendKeys(text);
        captureStepScreenshot("Type '" + text + "' in: " + locator.toString());
    }

    protected String getText(By locator) {
        String text = wait.until(ExpectedConditions.visibilityOfElementLocated(locator)).getText();
        captureStepScreenshot("Get text from: " + locator.toString());
        return text;
    }

    protected boolean isDisplayed(By locator) {
        try {
            boolean displayed = wait.until(ExpectedConditions.visibilityOfElementLocated(locator)).isDisplayed();
            captureStepScreenshot("Check displayed: " + locator.toString());
            return displayed;
        } catch (Exception e) {
            return false;
        }
    }

    protected void navigateTo(String url) {
        driver.get(url);
        captureStepScreenshot("Navigate to: " + url);
    }

    public String getPageTitle() {
        return driver.getTitle();
    }
}
```

---

# File 3: BaseTest.java (UPDATED)

**Location:** `src/test/java/com/traveleasy/base/BaseTest.java`

**Replace entire file with:**

```java
package com.traveleasy.base;

import com.traveleasy.config.ConfigReader;
import com.traveleasy.pages.BasePage;
import com.traveleasy.utils.ExtentReportManager;
import com.traveleasy.utils.ScreenshotUtil;
import com.aventstack.extentreports.ExtentTest;
import com.aventstack.extentreports.MediaEntityBuilder;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.edge.EdgeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.testng.ITestResult;
import org.testng.annotations.*;

import java.time.Duration;
import java.util.List;

public class BaseTest {
    protected WebDriver driver;
    protected ExtentTest extentTest;

    @BeforeMethod
    public void setUp(ITestResult result) {
        // Clear step screenshots from previous test
        BasePage.clearStepScreenshots();
        
        extentTest = ExtentReportManager.createTest(result.getMethod().getMethodName());
        String browser = ConfigReader.getBrowser();
        switch (browser.toLowerCase()) {
            case "chrome":
                ChromeOptions options = new ChromeOptions();
                options.addArguments("--enable-cookies");
                options.addArguments("--disable-blink-features=AutomationControlled");
                driver = new ChromeDriver(options);
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

        driver.manage().window().maximize();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
    }

    @AfterMethod
    public void tearDown(ITestResult result) {
        String testName = result.getMethod().getMethodName();
        
        if (result.getStatus() == ITestResult.FAILURE) {
            // Log failure message
            extentTest.fail("Test Failed: " + result.getThrowable().getMessage());
            
            // Save and attach ALL step screenshots to report
            List<ScreenshotUtil.StepScreenshotData> stepData = ScreenshotUtil.saveStepScreenshots(testName);
            
            for (ScreenshotUtil.StepScreenshotData step : stepData) {
                try {
                    // Attach each step screenshot to report using Base64
                    extentTest.info("Step " + step.stepNumber + ": " + step.description,
                        MediaEntityBuilder.createScreenCaptureFromBase64String(step.base64Image).build());
                } catch (Exception e) {
                    extentTest.info("Step " + step.stepNumber + ": " + step.description + " (screenshot failed)");
                }
            }
            
            // Take and attach failure screenshot
            String failureBase64 = ScreenshotUtil.takeScreenshotAsBase64(driver);
            try {
                extentTest.fail("Final State at Failure",
                    MediaEntityBuilder.createScreenCaptureFromBase64String(failureBase64).build());
            } catch (Exception e) {
                extentTest.info("Could not attach failure screenshot");
            }
            
            // Also save to file for reference
            ScreenshotUtil.takeScreenshot(driver, testName);
            
        } else if (result.getStatus() == ITestResult.SUCCESS) {
            extentTest.pass("Test Passed");
        } else {
            extentTest.skip("Test Skipped");
        }
        
        // Clear step screenshots after each test
        BasePage.clearStepScreenshots();
        
        if (driver != null) {
            driver.quit();
        }
    }

    @AfterSuite
    public void tearDownSuite() {
        ExtentReportManager.flush();
    }
}
```

---

# File 4: testng.xml (NEW FILE)

**Location:** Project root (`D:\java\SeleniumFramework\testng.xml`)

**Create this file:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="ShopEasy Test Suite" parallel="tests" thread-count="3">

    <test name="Login Tests">
        <classes>
            <class name="com.traveleasy.tests.LoginTest"/>
        </classes>
    </test>

    <test name="Products Tests">
        <classes>
            <class name="com.traveleasy.tests.ProductsTest"/>
        </classes>
    </test>

    <test name="Cart Tests">
        <classes>
            <class name="com.traveleasy.tests.CartTest"/>
        </classes>
    </test>

</suite>
```

---

# Jenkins Setup Steps

## 1. Download Jenkins
- Go to: https://www.jenkins.io/download/
- Download Windows LTS `.msi` installer

## 2. Install Jenkins
- Run installer
- Use port **8081** (if 8080 is taken)
- Select JDK 17 or 21
- Select "Run as LocalSystem"

## 3. Initial Setup
1. Open: http://localhost:8081
2. Get password: `C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword`
3. Install suggested plugins
4. Create admin user

## 4. Create Job
1. Click "New Item"
2. Name: `SeleniumFramework`
3. Select "Freestyle project" → OK

## 5. Configure Build
1. Go to "Build Steps"
2. Add "Execute Windows batch command"
3. Enter:
```batch
cd /d D:\java\SeleniumFramework
mvn clean test -DsuiteXmlFile=testng.xml
```
4. Save

## 6. Run
Click "Build Now" to run tests

---

# Summary of Changes

| File | Action | Purpose |
|------|--------|---------|
| ScreenshotUtil.java | NEW | Screenshot capture utilities |
| BasePage.java | UPDATED | Added step screenshot capture |
| BaseTest.java | UPDATED | Save screenshots on failure |
| testng.xml | NEW | Test suite configuration |
