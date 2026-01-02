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
