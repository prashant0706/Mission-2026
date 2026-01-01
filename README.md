# 📚 Selenium Java + QA Learning Notes
> Author: Prashant | Started: December 2025  
> Project: TravelEasy Test Automation Framework

---

## 📑 Table of Contents
0. [Java Fundamentals](#0-java-fundamentals) 
1. [Maven Basics](#1-maven-basics)
2. [Selenium Fundamentals](#2-selenium-fundamentals)
3. [TestNG Framework](#3-testng-framework)
4. [Locators](#4-locators)
5. [Page Object Model](#5-page-object-model)
6. [Waits](#6-waits)
7. [Jira Basics](#7-jira-basics)
8. [SQL for Testers](#8-sql-for-testers)
9. [DevOps Concepts](#9-devops-concepts)
10. [Best Practices](#10-best-practices)

---

## 0. Java Fundamentals

### What is Java?
Java is an **object-oriented programming language** that runs on the JVM (Java Virtual Machine). It's:
- ✅ Platform independent ("Write once, run anywhere")
- ✅ Strongly typed (variables must have declared types)
- ✅ Object-oriented (everything is an object)

### Java File Structure
```java
package com.traveleasy.tests;     // Package declaration (folder structure)

import org.openqa.selenium.*;     // Import statements (using other classes)

public class MyClass {            // Class declaration
    
    // Variables (data)
    int number = 10;
    String text = "Hello";
    
    // Methods (actions)
    public void doSomething() {
        System.out.println("Doing something!");
    }
}
```

### Variables and Data Types

#### Primitive Types (basic values)
```java
// Numeric
int age = 25;                  // Whole numbers (-2B to 2B)
long bigNumber = 9999999999L;  // Large whole numbers
double price = 19.99;          // Decimal numbers
float temp = 36.5f;            // Smaller decimals

// Text & Logic
char letter = 'A';             // Single character
boolean isActive = true;       // true or false

// Example in Selenium context
int timeout = 10;
boolean headless = false;
double expectedPrice = 4999.99;
```

#### Reference Types (objects)
```java
// String - text (most common!)
String url = "http://localhost:8080";
String email = "test@example.com";

// Arrays - list of items
String[] cities = {"Pune", "Mumbai", "Delhi"};
int[] numbers = {1, 2, 3, 4, 5};

// Objects
WebDriver driver = new ChromeDriver();
WebElement button = driver.findElement(By.id("submit"));
```

### Operators
```java
// Arithmetic
int sum = 5 + 3;        // 8
int diff = 10 - 4;      // 6
int product = 3 * 4;    // 12
int quotient = 10 / 3;  // 3 (integer division)
int remainder = 10 % 3; // 1 (modulo)

// Comparison (return boolean)
5 == 5    // true (equals)
5 != 3    // true (not equals)
5 > 3     // true (greater than)
5 < 3     // false (less than)
5 >= 5    // true (greater or equal)
5 <= 3    // false (less or equal)

// Logical
true && true   // true (AND - both must be true)
true || false  // true (OR - at least one true)
!true          // false (NOT - opposite)

// String comparison (IMPORTANT!)
String a = "hello";
String b = "hello";
a.equals(b);       // ✅ Correct way to compare strings
a == b;            // ❌ Wrong! Compares memory references
```

### Conditionals (if/else)
```java
// Basic if-else
int age = 18;

if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}

// Multiple conditions
String status = "CONFIRMED";

if (status.equals("CONFIRMED")) {
    System.out.println("Booking is confirmed");
} else if (status.equals("PENDING")) {
    System.out.println("Booking is pending");
} else if (status.equals("CANCELLED")) {
    System.out.println("Booking was cancelled");
} else {
    System.out.println("Unknown status");
}

// Ternary operator (short if-else)
String result = (age >= 18) ? "Adult" : "Minor";
```

### Loops
```java
// For loop - when you know how many times
for (int i = 0; i < 5; i++) {
    System.out.println("Iteration: " + i);  // 0, 1, 2, 3, 4
}

// Enhanced for loop - for arrays/lists
String[] browsers = {"Chrome", "Firefox", "Edge"};
for (String browser : browsers) {
    System.out.println("Testing on: " + browser);
}

// While loop - while condition is true
int count = 0;
while (count < 3) {
    System.out.println("Count: " + count);
    count++;  // Don't forget to increment!
}

// Selenium example: Wait for element
int attempts = 0;
while (attempts < 10) {
    if (driver.findElements(By.id("popup")).size() > 0) {
        break;  // Exit loop if found
    }
    Thread.sleep(500);
    attempts++;
}
```

### Methods (Functions)
```java
public class Calculator {
    
    // Method with no return value (void)
    public void printMessage(String message) {
        System.out.println(message);
    }
    
    // Method that returns a value
    public int add(int a, int b) {
        return a + b;
    }
    
    // Method with multiple parameters
    public double calculateTotal(double price, int quantity, double discount) {
        double total = price * quantity;
        return total - (total * discount / 100);
    }
    
    // Using the methods
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        calc.printMessage("Hello!");
        int sum = calc.add(5, 3);              // sum = 8
        double total = calc.calculateTotal(100, 2, 10);  // 180.0
    }
}
```

### Classes and Objects

#### What is a Class?
A **class** is a blueprint/template. An **object** is an instance of that class.

```java
// Class = Blueprint for a Car
public class Car {
    // Properties (what it HAS)
    String brand;
    String color;
    int speed;
    
    // Constructor (how to CREATE it)
    public Car(String brand, String color) {
        this.brand = brand;
        this.color = color;
        this.speed = 0;
    }
    
    // Methods (what it DOES)
    public void accelerate() {
        speed += 10;
        System.out.println(brand + " accelerating. Speed: " + speed);
    }
    
    public void brake() {
        speed -= 10;
        System.out.println(brand + " braking. Speed: " + speed);
    }
}

// Creating Objects (instances)
Car myCar = new Car("Toyota", "Red");
Car yourCar = new Car("Honda", "Blue");

myCar.accelerate();    // Toyota accelerating. Speed: 10
yourCar.accelerate();  // Honda accelerating. Speed: 10
```

### Access Modifiers
```java
public class Example {
    public String publicVar;      // Accessible from anywhere
    private String privateVar;    // Only within this class
    protected String protectedVar; // This class + subclasses
    String defaultVar;            // Same package only
}
```

| Modifier | Same Class | Same Package | Subclass | Everywhere |
|----------|------------|--------------|----------|------------|
| public | ✅ | ✅ | ✅ | ✅ |
| protected | ✅ | ✅ | ✅ | ❌ |
| default | ✅ | ✅ | ❌ | ❌ |
| private | ✅ | ❌ | ❌ | ❌ |

### Constructors
```java
public class User {
    private String name;
    private String email;
    
    // Default constructor (no parameters)
    public User() {
        this.name = "Guest";
        this.email = "guest@example.com";
    }
    
    // Parameterized constructor
    public User(String name, String email) {
        this.name = name;      // 'this' refers to the object's variable
        this.email = email;
    }
    
    // Getters (to READ private variables)
    public String getName() {
        return name;
    }
    
    // Setters (to WRITE private variables)
    public void setName(String name) {
        this.name = name;
    }
}

// Using constructors
User guest = new User();                              // Uses default
User john = new User("John", "john@email.com");       // Uses parameterized
```

### Inheritance (Extending Classes)
```java
// Parent class (base/super class)
public class Animal {
    protected String name;
    
    public void eat() {
        System.out.println(name + " is eating");
    }
}

// Child class (derived/sub class)
public class Dog extends Animal {
    
    public Dog(String name) {
        this.name = name;  // Inherited from Animal
    }
    
    // Dog-specific method
    public void bark() {
        System.out.println(name + " says Woof!");
    }
    
    // Override parent method
    @Override
    public void eat() {
        System.out.println(name + " is eating dog food");
    }
}

// Usage
Dog buddy = new Dog("Buddy");
buddy.eat();    // "Buddy is eating dog food"
buddy.bark();   // "Buddy says Woof!"
```

### Interfaces
```java
// Interface = Contract (defines WHAT, not HOW)
public interface Drivable {
    void start();
    void stop();
    void accelerate(int speed);
}

// Class implementing interface
public class Car implements Drivable {
    
    @Override
    public void start() {
        System.out.println("Car started");
    }
    
    @Override
    public void stop() {
        System.out.println("Car stopped");
    }
    
    @Override
    public void accelerate(int speed) {
        System.out.println("Accelerating to " + speed);
    }
}

// WebDriver is an interface!
// ChromeDriver, FirefoxDriver implement it
WebDriver driver = new ChromeDriver();
```

### Exception Handling
```java
try {
    // Code that might fail
    WebElement element = driver.findElement(By.id("doesNotExist"));
    element.click();
    
} catch (NoSuchElementException e) {
    // Handle specific exception
    System.out.println("Element not found: " + e.getMessage());
    
} catch (Exception e) {
    // Handle any other exception
    System.out.println("Something went wrong: " + e.getMessage());
    
} finally {
    // Always runs (cleanup code)
    driver.quit();
}
```

### Common String Methods
```java
String text = "Hello World";

text.length();              // 11 (character count)
text.toLowerCase();         // "hello world"
text.toUpperCase();         // "HELLO WORLD"
text.trim();                // Remove whitespace from ends
text.contains("World");     // true
text.startsWith("Hello");   // true
text.endsWith("World");     // true
text.substring(0, 5);       // "Hello"
text.replace("World", "Java"); // "Hello Java"
text.split(" ");            // ["Hello", "World"]
text.isEmpty();             // false
text.equals("Hello World"); // true
```

### Collections (Lists)
```java
import java.util.ArrayList;
import java.util.List;

// Create a list
List<String> fruits = new ArrayList<>();

// Add items
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

// Access items
String first = fruits.get(0);    // "Apple"

// Size
int count = fruits.size();       // 3

// Check if contains
boolean hasApple = fruits.contains("Apple");  // true

// Loop through
for (String fruit : fruits) {
    System.out.println(fruit);
}

// Remove item
fruits.remove("Banana");

// Selenium example
List<WebElement> links = driver.findElements(By.tagName("a"));
for (WebElement link : links) {
    System.out.println(link.getText());
}
```

### Static Keyword
```java
public class MathUtils {
    
    // Static variable - shared by ALL objects
    public static int counter = 0;
    
    // Static method - belongs to CLASS, not object
    public static int add(int a, int b) {
        return a + b;
    }
}

// Call without creating object
int result = MathUtils.add(5, 3);  // 8
MathUtils.counter++;
```

### The 'this' Keyword
```java
public class Person {
    private String name;
    
    public Person(String name) {
        this.name = name;  // 'this.name' = object's variable
                           // 'name' = parameter passed in
    }
    
    public Person setName(String name) {
        this.name = name;
        return this;  // Return the object itself (method chaining)
    }
}
```

---

## 1. Maven Basics

### What is Maven?
Maven is a **build automation tool** for Java projects. It handles:
- ✅ Dependency management (auto-downloads libraries)
- ✅ Project structure standardization
- ✅ Build lifecycle (compile → test → package)
- ✅ Running tests

### Key Files
| File | Purpose |
|------|---------|
| `pom.xml` | Project configuration, dependencies |
| `src/main/java` | Application code |
| `src/test/java` | Test code |
| `src/main/resources` | Config files |

### Key Maven Commands
```bash
mvn clean           # Delete target folder
mvn compile         # Compile source code
mvn test            # Run all tests
mvn clean test      # Clean and run tests
mvn install         # Build and install to local repo
```

### pom.xml Structure
```xml
<project>
    <groupId>com.company</groupId>      <!-- Company/org name -->
    <artifactId>ProjectName</artifactId> <!-- Project name -->
    <version>1.0-SNAPSHOT</version>      <!-- Version -->
    
    <dependencies>
        <!-- Libraries your project needs -->
    </dependencies>
</project>
```

---

## 2. Selenium Fundamentals

### What is Selenium WebDriver?
Selenium WebDriver is a **browser automation tool** that allows you to:
- Open browsers programmatically
- Navigate to URLs
- Find and interact with elements
- Verify page content

### WebDriver Hierarchy
```
WebDriver (Interface)
    ├── ChromeDriver
    ├── FirefoxDriver
    ├── EdgeDriver
    └── SafariDriver
```

### Basic WebDriver Methods
```java
// Navigation
driver.get("https://example.com");       // Open URL
driver.navigate().back();                 // Go back
driver.navigate().forward();              // Go forward
driver.navigate().refresh();              // Refresh page

// Browser Info
driver.getTitle();                        // Get page title
driver.getCurrentUrl();                   // Get current URL
driver.getPageSource();                   // Get HTML source

// Window Management
driver.manage().window().maximize();      // Maximize window
driver.manage().window().minimize();      // Minimize window
driver.manage().window().fullscreen();    // Fullscreen

// Closing
driver.close();                           // Close current tab
driver.quit();                            // Close all tabs + driver
```

### Example: First Test
```java
WebDriverManager.chromedriver().setup();  // Setup driver
WebDriver driver = new ChromeDriver();     // Open Chrome
driver.get("http://localhost:8080");       // Navigate
System.out.println(driver.getTitle());     // Print title
driver.quit();                             // Close
```

---

## 3. TestNG Framework

### What is TestNG?
TestNG is a **testing framework** (alternative to JUnit) with more features:
- Annotations for test lifecycle
- Test grouping
- Data-driven testing
- Parallel execution
- HTML reports

### TestNG Annotations (Execution Order)
```
@BeforeSuite    → Runs once before all tests in suite
  @BeforeTest   → Runs before each <test> tag in testng.xml
    @BeforeClass  → Runs once before first test in class
      @BeforeMethod → Runs before EACH @Test method
        @Test       → The actual test
      @AfterMethod  → Runs after EACH @Test method
    @AfterClass   → Runs once after last test in class
  @AfterTest    → Runs after each <test> tag
@AfterSuite     → Runs once after all tests
```

### Common Annotations
```java
@Test                           // Marks method as test
@Test(priority = 1)             // Run order (lower = first)
@Test(enabled = false)          // Skip this test
@Test(groups = {"smoke"})       // Group tests
@Test(dependsOnMethods = {"login"})  // Dependencies
@Test(dataProvider = "data")    // Data-driven testing
```

### Assertions
```java
import org.testng.Assert;

Assert.assertEquals(actual, expected);      // Check equality
Assert.assertTrue(condition);               // Check true
Assert.assertFalse(condition);              // Check false
Assert.assertNotNull(object);               // Check not null
Assert.fail("Message");                     // Force fail
```

---

## 4. Locators

### How to Find Elements
Selenium needs to **locate elements** on the page before interacting with them.

### Locator Types (Best to Worst)
| Priority | Locator | Example | When to Use |
|----------|---------|---------|-------------|
| 1 | ID | `By.id("username")` | Always prefer if available |
| 2 | Name | `By.name("email")` | Good for forms |
| 3 | CSS Selector | `By.cssSelector("#login .btn")` | Flexible & fast |
| 4 | XPath | `By.xpath("//input[@id='user']")` | When others fail |
| 5 | Link Text | `By.linkText("Click Here")` | For `<a>` tags |
| 6 | Class Name | `By.className("submit-btn")` | If class is unique |
| 7 | Tag Name | `By.tagName("input")` | Rarely used |

### CSS Selector Syntax
```css
#id                    /* By ID */
.class                 /* By class */
tag                    /* By tag name */
tag#id                 /* Tag with ID */
tag.class              /* Tag with class */
[attribute=value]      /* By attribute */
parent > child         /* Direct child */
parent child           /* Any descendant */
element:first-child    /* First child */
```

### XPath Syntax
```xpath
//tag                           # Any tag
//tag[@attribute='value']       # By attribute
//tag[contains(@attr,'partial')] # Partial match
//tag[text()='Exact Text']      # By text content
//tag[contains(text(),'partial')] # Partial text
//parent/child                  # Direct child
//parent//descendant            # Any descendant
(//tag)[1]                      # First occurrence
```

### Finding Elements in Code
```java
// Single element
WebElement element = driver.findElement(By.id("username"));

// Multiple elements
List<WebElement> elements = driver.findElements(By.className("item"));

// Check if element exists
boolean exists = driver.findElements(By.id("popup")).size() > 0;
```

### Common Element Actions
```java
element.click();                     // Click
element.sendKeys("text");            // Type text
element.clear();                     // Clear field
element.getText();                   // Get visible text
element.getAttribute("value");       // Get attribute
element.isDisplayed();               // Check visible
element.isEnabled();                 // Check enabled
element.isSelected();                // Check selected (checkbox/radio)
```

---

## 5. Page Object Model

### What is POM?
Page Object Model is a **design pattern** where:
- Each web page has a corresponding Java class
- Elements and actions are encapsulated in that class
- Tests use page objects instead of raw Selenium calls

### Why Use POM?
| Without POM | With POM |
|-------------|----------|
| Code duplication | Reusable page classes |
| Hard to maintain | Change in one place |
| Tests are messy | Clean, readable tests |

### POM Structure
```
pages/
├── BasePage.java       ← Common methods
├── LoginPage.java      ← Login page elements/actions
├── HomePage.java       ← Home page elements/actions
└── FlightsPage.java    ← Flights page elements/actions

tests/
├── BaseTest.java       ← Setup/teardown
├── LoginTest.java      ← Login tests
└── BookingTest.java    ← Booking tests
```

### Example: LoginPage
```java
public class LoginPage {
    WebDriver driver;
    
    // Locators
    By emailInput = By.id("email");
    By passwordInput = By.id("password");
    By loginButton = By.id("login-btn");
    
    // Constructor
    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }
    
    // Actions
    public void enterEmail(String email) {
        driver.findElement(emailInput).sendKeys(email);
    }
    
    public void enterPassword(String password) {
        driver.findElement(passwordInput).sendKeys(password);
    }
    
    public HomePage clickLogin() {
        driver.findElement(loginButton).click();
        return new HomePage(driver);  // Return next page
    }
    
    // Combined action
    public HomePage login(String email, String password) {
        enterEmail(email);
        enterPassword(password);
        return clickLogin();
    }
}
```

---

## 6. Waits

### Why Waits?
Web pages load dynamically. Without waits, Selenium may try to interact with elements that haven't loaded yet → **NoSuchElementException**!

### Types of Waits

#### 1. Implicit Wait (Global)
```java
// Set once, applies to all findElement calls
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
```
- ✅ Simple to use
- ❌ Applies to ALL elements
- ❌ May slow down tests

#### 2. Explicit Wait (Recommended)
```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));

// Wait for element to be visible
WebElement element = wait.until(
    ExpectedConditions.visibilityOfElementLocated(By.id("result"))
);

// Wait for element to be clickable
wait.until(ExpectedConditions.elementToBeClickable(By.id("btn")));

// Wait for text to appear
wait.until(ExpectedConditions.textToBePresentInElement(element, "Success"));
```
- ✅ Specific to element/condition
- ✅ More control
- ❌ More code

#### 3. Fluent Wait (Advanced)
```java
Wait<WebDriver> wait = new FluentWait<>(driver)
    .withTimeout(Duration.ofSeconds(30))
    .pollingEvery(Duration.ofMillis(500))
    .ignoring(NoSuchElementException.class);
```

### Common Expected Conditions
```java
ExpectedConditions.visibilityOfElementLocated(locator)
ExpectedConditions.elementToBeClickable(locator)
ExpectedConditions.presenceOfElementLocated(locator)
ExpectedConditions.invisibilityOfElementLocated(locator)
ExpectedConditions.titleContains("text")
ExpectedConditions.urlContains("path")
ExpectedConditions.alertIsPresent()
```

### ⚠️ Never Use Thread.sleep()!
```java
Thread.sleep(5000);  // BAD! Wastes time, unreliable
```

---

## 7. Jira Basics

### What is Jira?
Jira is a **project management tool** for Agile teams. Used for:
- 📋 Tracking work items (stories, tasks, bugs)
- 🏃 Managing sprints
- 🐛 Bug tracking
- 📊 Reporting progress

### Jira Terminology
| Term | Meaning |
|------|---------|
| **Project** | Container for all work (e.g., "TravelEasy") |
| **Issue** | A work item (story, bug, task) |
| **Epic** | Large feature broken into stories |
| **Story** | User feature ("As a user, I want...") |
| **Task** | Technical work item |
| **Bug** | Defect to fix |
| **Sprint** | Time-boxed iteration (usually 2 weeks) |
| **Backlog** | Pool of unplanned work |

### Issue Workflow
```
To Do → In Progress → In Review → Done
                ↓
            Blocked
```

### Story Template
```
Title: [Feature] - Short description

Description:
As a [type of user],
I want [feature/action],
So that [benefit/reason].

Acceptance Criteria:
- [ ] Criteria 1
- [ ] Criteria 2
- [ ] Criteria 3

Story Points: 3
Sprint: Sprint 1
Assignee: Prashant
```

### Bug Report Template
```
Title: [BUG] - Short description

Environment:
- Browser: Chrome 120
- OS: Windows 11
- URL: http://localhost:8080/travel

Steps to Reproduce:
1. Go to login page
2. Enter invalid email
3. Click Login

Expected Result:
Error message "Invalid email" should appear

Actual Result:
Page crashes with 500 error

Severity: High
Priority: P1
Attachments: [screenshot.png]
```

---

## 8. SQL for Testers

### Why SQL for Testing?
- Verify data saved correctly after actions
- Setup test data before tests
- Validate backend vs frontend
- Debug issues

### Basic SQL Queries
```sql
-- Select all records
SELECT * FROM users;

-- Select specific columns
SELECT name, email FROM users;

-- Filter with WHERE
SELECT * FROM bookings WHERE status = 'CONFIRMED';

-- Multiple conditions
SELECT * FROM bookings 
WHERE status = 'CONFIRMED' 
AND user_id = 1;

-- Sort results
SELECT * FROM flights ORDER BY price ASC;

-- Count records
SELECT COUNT(*) FROM bookings WHERE user_id = 1;

-- Insert data
INSERT INTO users (name, email, password) 
VALUES ('Test', 'test@email.com', 'pass123');

-- Update data
UPDATE bookings SET status = 'CANCELLED' WHERE id = 5;

-- Delete data
DELETE FROM bookings WHERE id = 5;
```

### Join Tables
```sql
-- Get bookings with user info
SELECT b.*, u.name, u.email
FROM bookings b
JOIN users u ON b.user_id = u.id;
```

### Testing Use Cases
```sql
-- Verify new user created
SELECT * FROM users WHERE email = 'newuser@test.com';

-- Check booking status after cancellation
SELECT status FROM bookings WHERE booking_reference = 'TRV-12345';

-- Count user's total bookings
SELECT COUNT(*) FROM bookings WHERE user_email = 'test@example.com';
```

---

## 9. DevOps Concepts

### What is DevOps?
DevOps is a practice that combines **Development** and **Operations** for faster, reliable software delivery.

### Key DevOps Concepts

#### Git (Version Control)
```bash
git init                  # Initialize repo
git add .                 # Stage all changes
git commit -m "message"   # Commit changes
git push origin main      # Push to remote
git pull                  # Get latest changes
git branch feature-1      # Create branch
git checkout feature-1    # Switch branch
git merge feature-1       # Merge branch
```

#### CI/CD Pipeline
```
Developer pushes code
        ↓
CI Server (Jenkins/GitHub Actions)
        ↓
    Build → Test → Deploy
        ↓
   Production
```

#### Docker Basics
```bash
# Pull an image
docker pull selenium/standalone-chrome

# Run container
docker run -d -p 4444:4444 selenium/standalone-chrome

# List running containers
docker ps

# Stop container
docker stop container_id
```

### Jenkins Basics
Jenkins is a **CI/CD automation server** that:
- Runs tests automatically on code push
- Builds projects
- Deploys applications

---

## 10. Best Practices

### Test Code Best Practices
1. ✅ Use meaningful test names
2. ✅ One assertion per test (ideally)
3. ✅ Independent tests (no dependencies)
4. ✅ Clean up after tests
5. ✅ Use Page Object Model
6. ✅ Explicit waits over implicit
7. ✅ Avoid hard-coded data

### Naming Conventions
```java
// Test class: [Feature]Test
public class LoginTest { }

// Test method: test[Action][Scenario]
@Test
public void testLoginWithValidCredentials() { }

@Test
public void testLoginWithInvalidPassword() { }
```

### Project Structure
```
src/
├── main/java/
│   ├── config/ConfigReader.java
│   ├── pages/
│   │   ├── BasePage.java
│   │   ├── LoginPage.java
│   │   └── HomePage.java
│   └── utils/
│       ├── WaitHelper.java
│       └── ScreenshotUtil.java
│
├── test/java/
│   ├── base/BaseTest.java
│   └── tests/
│       ├── LoginTest.java
│       └── BookingTest.java
│
└── resources/
    ├── config.properties
    └── testng.xml
```

---

## 📝 Quick Reference Card

### Selenium Commands
| Action | Code |
|--------|------|
| Open URL | `driver.get("url")` |
| Find element | `driver.findElement(By.id("x"))` |
| Click | `element.click()` |
| Type | `element.sendKeys("text")` |
| Get text | `element.getText()` |
| Wait | `WebDriverWait + ExpectedConditions` |

### TestNG Annotations
| Annotation | Purpose |
|------------|---------|
| `@Test` | Test method |
| `@BeforeMethod` | Before each test |
| `@AfterMethod` | After each test |
| `@BeforeClass` | Before all tests in class |

### Locator Priority
1. ID → 2. Name → 3. CSS → 4. XPath

---

## 11. Interview Questions & Answers 🎯

### 📌 How to Answer Interview Questions

**STAR Method** (for behavioral questions):
- **S**ituation: Describe the context
- **T**ask: What was your responsibility
- **A**ction: What you did
- **R**esult: The outcome

**Technical Questions**: Be specific, give examples, mention real projects!

---

### 🔷 Java Interview Questions

#### Q1: What is the difference between `==` and `.equals()` in Java?
**Answer:**
> "`==` compares **memory references** (whether two variables point to the same object in memory), while `.equals()` compares the **actual content/values** of objects.
>
> For example, with Strings:
> ```java
> String a = new String("hello");
> String b = new String("hello");
> a == b       // false (different objects in memory)
> a.equals(b)  // true (same content)
> ```
> In my Selenium tests, I always use `.equals()` when comparing text from web elements."

---

#### Q2: What is the difference between `public`, `private`, and `protected`?
**Answer:**
> "These are **access modifiers** that control visibility:
> - `public`: Accessible from anywhere
> - `private`: Only within the same class
> - `protected`: Same class + subclasses + same package
> - Default (no modifier): Same package only
>
> In Page Object Model, I typically make locators `private` and methods `public`, following encapsulation principles."

---

#### Q3: What is Object-Oriented Programming (OOP)?
**Answer:**
> "OOP is a programming paradigm based on 4 pillars:
> 1. **Encapsulation**: Hiding internal details (private variables, public getters/setters)
> 2. **Inheritance**: Child classes inherit from parent classes (`extends`)
> 3. **Polymorphism**: Same method behaving differently (method overriding)
> 4. **Abstraction**: Hiding complexity, showing only essential features (interfaces)
>
> In my framework, I use inheritance with BasePage and BaseTest classes, and all page classes extend them."

---

#### Q4: What is the difference between `interface` and `abstract class`?
**Answer:**
> "An **interface** defines a contract with only method signatures (what to do), while an **abstract class** can have both abstract methods and implemented methods (how to do it).
>
> - Interface: `implements`, 100% abstraction, multiple interfaces allowed
> - Abstract class: `extends`, 0-100% abstraction, only one parent allowed
>
> `WebDriver` is an interface - ChromeDriver and FirefoxDriver implement it."

---

#### Q5: What is exception handling? What are `try`, `catch`, `finally`?
**Answer:**
> "`try` block contains code that might throw an exception. `catch` block handles specific exceptions. `finally` block always executes for cleanup.
>
> ```java
> try {
>     driver.findElement(By.id("invalid")).click();
> } catch (NoSuchElementException e) {
>     System.out.println("Element not found");
> } finally {
>     driver.quit();  // Always runs
> }
> ```
> In my framework, I use try-catch in utility methods and take screenshots in catch blocks."

---

#### Q6: What is the difference between `ArrayList` and `Array`?
**Answer:**
> "Arrays have **fixed size** declared at creation. ArrayList is **dynamic** and can grow or shrink.
>
> ```java
> int[] arr = new int[5];          // Fixed size 5
> ArrayList<Integer> list = new ArrayList<>();  // Dynamic
> list.add(1);  // Can keep adding
> ```
> In Selenium, `findElements()` returns a List, not an array."

---

### 🔷 Selenium Interview Questions

#### Q1: What is Selenium WebDriver?
**Answer:**
> "Selenium WebDriver is a **browser automation tool** that provides APIs to interact with web browsers programmatically. It supports multiple browsers (Chrome, Firefox, Edge) and multiple languages (Java, Python, C#).
>
> WebDriver directly communicates with the browser using browser-specific drivers like ChromeDriver."

---

#### Q2: What are the different types of locators in Selenium?
**Answer:**
> "Selenium provides 8 locator types:
> 1. **ID** (fastest, most reliable)
> 2. **Name**
> 3. **Class Name**
> 4. **Tag Name**
> 5. **Link Text** (for anchor tags)
> 6. **Partial Link Text**
> 7. **CSS Selector** (flexible, fast)
> 8. **XPath** (most powerful, can traverse DOM)
>
> I prioritize ID first, then CSS Selector, and use XPath only when necessary."

---

#### Q3: What is the difference between `findElement()` and `findElements()`?
**Answer:**
> "`findElement()` returns a **single WebElement** and throws `NoSuchElementException` if not found.
>
> `findElements()` returns a **List of WebElements** and returns an empty list (not exception) if none found.
>
> I use `findElements().size() > 0` to check if an element exists without throwing exceptions."

---

#### Q4: What are the different types of waits in Selenium?
**Answer:**
> "There are 3 types:
>
> 1. **Implicit Wait**: Global wait, applies to all findElement calls
>    ```java
>    driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
>    ```
>
> 2. **Explicit Wait**: Waits for specific condition
>    ```java
>    WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
>    wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("element")));
>    ```
>
> 3. **Fluent Wait**: Explicit wait with polling interval and exception ignoring
>
> I prefer Explicit Wait because it's more precise and efficient."

---

#### Q5: What is Page Object Model (POM)?
**Answer:**
> "POM is a **design pattern** where each web page has a corresponding Java class. The class contains:
> - Element locators (private)
> - Page actions as methods (public)
>
> Benefits:
> - Code reusability
> - Easy maintenance (change in one place)
> - Readable tests
>
> Example: `LoginPage` class has methods like `enterUsername()`, `enterPassword()`, `clickLogin()`."

---

#### Q6: How do you handle dynamic elements?
**Answer:**
> "For dynamic elements, I use:
> 1. **Partial attribute matching**: `contains()`, `starts-with()`
>    ```java
>    By.xpath("//div[contains(@id,'dynamic_')]")
>    ```
> 2. **CSS partial match**: `[id*='partial']`
> 3. **Explicit waits**: Wait for element to be present
> 4. **Relative XPath**: Find stable parent, then navigate to child
>
> In one project, IDs were dynamically generated, so I used data-testid attributes."

---

#### Q7: How do you handle alerts/popups?
**Answer:**
> ```java
> // Switch to alert
> Alert alert = driver.switchTo().alert();
>
> // Get alert text
> String text = alert.getText();
>
> // Accept (OK)
> alert.accept();
>
> // Dismiss (Cancel)
> alert.dismiss();
>
> // Enter text in prompt
> alert.sendKeys("text");
> ```

---

#### Q8: How do you handle frames/iframes?
**Answer:**
> ```java
> // Switch by index
> driver.switchTo().frame(0);
>
> // Switch by name or ID
> driver.switchTo().frame("frameName");
>
> // Switch by WebElement
> driver.switchTo().frame(driver.findElement(By.id("frameId")));
>
> // Switch back to main content
> driver.switchTo().defaultContent();
> ```

---

#### Q9: How do you handle multiple windows/tabs?
**Answer:**
> ```java
> // Get current window handle
> String mainWindow = driver.getWindowHandle();
>
> // Get all window handles
> Set<String> allWindows = driver.getWindowHandles();
>
> // Switch to new window
> for (String window : allWindows) {
>     if (!window.equals(mainWindow)) {
>         driver.switchTo().window(window);
>     }
> }
>
> // Switch back
> driver.switchTo().window(mainWindow);
> ```

---

#### Q10: What is the difference between `close()` and `quit()`?
**Answer:**
> "`close()` closes only the **current browser window/tab**.
>
> `quit()` closes **all browser windows** and terminates the WebDriver session.
>
> I always use `quit()` in `@AfterMethod` to ensure proper cleanup."

---

### 🔷 TestNG Interview Questions

#### Q1: What is TestNG? Why use it over JUnit?
**Answer:**
> "TestNG is a testing framework. Advantages over JUnit:
> - **Annotations** for test lifecycle (@BeforeSuite, @BeforeTest, @BeforeClass, @BeforeMethod)
> - **Parallel execution** out of the box
> - **Grouping** tests (smoke, regression)
> - **Data-driven testing** with @DataProvider
> - **Dependency** management between tests
> - **Better reporting**"

---

#### Q2: Explain TestNG annotation execution order.
**Answer:**
> ```
> @BeforeSuite
>   @BeforeTest
>     @BeforeClass
>       @BeforeMethod
>         @Test
>       @AfterMethod
>     @AfterClass
>   @AfterTest
> @AfterSuite
> ```
> I use @BeforeMethod for browser setup and @AfterMethod for teardown."

---

#### Q3: What is @DataProvider?
**Answer:**
> "@DataProvider enables **data-driven testing** by providing multiple sets of test data.
> ```java
> @DataProvider(name = "loginData")
> public Object[][] getLoginData() {
>     return new Object[][] {
>         {"user1@test.com", "pass1"},
>         {"user2@test.com", "pass2"},
>         {"invalid@test.com", "wrongpass"}
>     };
> }
>
> @Test(dataProvider = "loginData")
> public void testLogin(String email, String password) {
>     loginPage.login(email, password);
> }
> ```
> The test runs 3 times with different data."

---

#### Q4: How do you run tests in parallel?
**Answer:**
> "In testng.xml:
> ```xml
> <suite name="Suite" parallel="tests" thread-count="3">
>     <test name="ChromeTest">
>         <parameter name="browser" value="chrome"/>
>         <classes>
>             <class name="com.test.LoginTest"/>
>         </classes>
>     </test>
> </suite>
> ```
> parallel options: `tests`, `classes`, `methods`"

---

### 🔷 SQL Interview Questions

#### Q1: What is the difference between WHERE and HAVING?
**Answer:**
> "**WHERE** filters rows before grouping.
> **HAVING** filters groups after GROUP BY.
> ```sql
> SELECT city, COUNT(*) as bookings
> FROM bookings
> WHERE status = 'CONFIRMED'
> GROUP BY city
> HAVING COUNT(*) > 10;
> ```

---

#### Q2: What are JOINs? Types?
**Answer:**
> "JOIN combines rows from 2+ tables.
> - **INNER JOIN**: Only matching rows from both tables
> - **LEFT JOIN**: All from left + matching from right
> - **RIGHT JOIN**: All from right + matching from left
> - **FULL JOIN**: All from both tables
> ```sql
> SELECT u.name, b.booking_reference
> FROM users u
> LEFT JOIN bookings b ON u.id = b.user_id;
> ```

---

#### Q3: What is the difference between DELETE, TRUNCATE, DROP?
**Answer:**
> "- **DELETE**: Removes specific rows, can use WHERE, logged, can rollback
> - **TRUNCATE**: Removes all rows, faster, minimal logging, cannot rollback
> - **DROP**: Removes entire table structure and data"

---

### 🔷 Jira Interview Questions

#### Q1: What is Agile/Scrum?
**Answer:**
> "Agile is an iterative development methodology. Scrum is a framework:
> - Work in **Sprints** (2-4 weeks)
> - **Daily standups** (15 min)
> - **Sprint planning** at start
> - **Sprint review/retrospective** at end
> - Roles: Product Owner, Scrum Master, Dev Team"

---

#### Q2: What is a User Story?
**Answer:**
> "A user story describes a feature from user perspective:
> **'As a [user type], I want [feature], so that [benefit]'**
>
> Example: 'As a customer, I want to filter flights by price, so that I can find affordable options.'
>
> Stories have **acceptance criteria** and **story points** for estimation."

---

#### Q3: How do you write a good bug report?
**Answer:**
> "A good bug report includes:
> - **Clear title**: [BUG] Short description
> - **Environment**: Browser, OS, URL
> - **Steps to reproduce**: Numbered steps
> - **Expected result**: What should happen
> - **Actual result**: What actually happened
> - **Severity/Priority**: Critical/High/Medium/Low
> - **Screenshots/videos**: Visual proof"

---

### 🔷 DevOps Interview Questions

#### Q1: What is CI/CD?
**Answer:**
> "**CI (Continuous Integration)**: Developers merge code frequently, automated builds and tests run on each merge.
>
> **CD (Continuous Delivery/Deployment)**: Automatically deploy to staging/production after tests pass.
>
> Pipeline: Code → Build → Test → Deploy"

---

#### Q2: What is Docker?
**Answer:**
> "Docker is a **containerization platform**. Containers package applications with all dependencies, ensuring consistent environments.
>
> - **Image**: Blueprint/template
> - **Container**: Running instance of image
>
> For Selenium, I use `selenium/standalone-chrome` image for headless testing in CI."

---

#### Q3: What Git commands do you use?
**Answer:**
> "Daily commands:
> - `git pull`: Get latest changes
> - `git add .`: Stage changes
> - `git commit -m "message"`: Commit with message
> - `git push`: Push to remote
> - `git branch feature-x`: Create branch
> - `git checkout feature-x`: Switch branch
> - `git merge`: Merge branches"

---

### 🔷 Behavioral Questions

#### Q1: Tell me about yourself.
**Answer:**
> "I'm a QA professional with experience in manual and automation testing. I specialize in Selenium with Java, following Page Object Model and data-driven frameworks. I've worked on [project/domain], where I reduced regression testing time by X% through automation. I'm passionate about quality and continuously learning new tools like [current learning]."

---

#### Q2: Describe a challenging bug you found.
**Answer (STAR method):**
> "**Situation**: In my e-commerce project, users reported random checkout failures.
>
> **Task**: I needed to identify the root cause.
>
> **Action**: I created detailed test cases, captured network logs, and found the issue only occurred with specific payment combinations during peak hours. I traced it to a race condition.
>
> **Result**: The bug was fixed, checkout success rate improved by 15%, and I added new test cases to prevent regression."

---

#### Q3: How do you prioritize test cases?
**Answer:**
> "I prioritize based on:
> 1. **Risk**: High-impact areas first
> 2. **Frequency of use**: Most-used features
> 3. **Business criticality**: Revenue-generating flows
> 4. **Recent changes**: New/modified code
>
> I categorize into Smoke (P0), Critical (P1), and Regression (P2) suites."

---
Q: What type of framework have you used?

A: "I've built a Hybrid Framework combining Page Object Model with Data-Driven approach.

Page Objects encapsulate locators and actions for each page
Test data comes from Excel/properties files
BaseTest handles setup/teardown
Utilities handle common operations like waits and screenshots
We use TestNG for execution and ExtentReports for reporting."
--

---

## 📝 Interview Tips

1. ✅ **Be specific**: Use real examples from projects
2. ✅ **Show code**: Explain with code snippets
3. ✅ **Admit gaps**: "I haven't used X, but I'm eager to learn"
4. ✅ **Ask questions**: Shows interest and engagement
5. ✅ **Practice**: Mock interviews help!

---



*Notes will be updated as we learn more!* 📖
