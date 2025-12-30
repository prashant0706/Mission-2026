# 📚 Selenium Java + QA Learning Notes
> Author: Prashant | Started: December 2025  
> Project: TravelEasy Test Automation Framework

---

## 📑 Table of Contents
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

*Notes will be updated as we learn more!* 📖
