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

