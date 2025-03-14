# OpenCart Login Automation with Selenium and Cucumber

## 📌 Overview
This project automates the login functionality of the OpenCart e-commerce website using **Selenium WebDriver**, **Cucumber (BDD)**, and **TestNG** for parallel execution.

## 🛠 Tech Stack
- **Java** (Programming Language)
- **Selenium WebDriver** (UI Automation)
- **Cucumber (BDD)** (Behavior-Driven Testing)
- **TestNG** (Parallel Execution & Reporting)
- **Maven** (Build Tool)

## 📂 Project Structure
```
src
 ├── main
 │   ├── java
 │   │   ├── com.opencart.pages          # Page Object Model (POM) classes
 │   │   ├── com.opencart.utils          # Utility classes
 │   ├── resources
 ├── test
 │   ├── java
 │   │   ├── com.opencart.stepDefinitions # Step Definitions for Cucumber
 │   │   ├── runner                       # Test Runner
 │   ├── resources
 │   │   ├── features                     # Cucumber feature files
 │   │   ├── testng.xml                    # TestNG Configuration
```

## 🌟 Features Covered
- ✅ Successful login with valid credentials  
- ✅ Unsuccessful login with invalid or empty credentials (Scenario Outline)  
- ✅ Navigating to the "Forgotten Password" page  

## 📝 **Feature File: Login Functionality**
```gherkin
Feature: Login Functionality for OpenCart E-commerce Website
  As a user of the OpenCart website
  I want to be able to log in with my account
  So that I can access my account-related features and manage my orders

  Background:
    Given I am on the OpenCart login page

  Scenario: Successful login with valid credentials
    Given I have entered a valid username and password
    When I click on the login button
    Then I should be logged in successfully

  Scenario Outline: Unsuccessful login with invalid or empty credentials
    Given I have entered invalid "<username>" and "<password>"
    When I click on the login button
    Then I should see an error message indicating "<error_message>"

    Examples:
      | username          | password        | error_message                                         |
      | invalid@email.com | invalidPassword | Warning: No match for E-Mail Address and/or Password. |
      | abcccc            | validPassword   | Warning: No match for E-Mail Address and/or Password. |
      | valid@email.com   | abccc           | Warning: No match for E-Mail Address and/or Password  |

  Scenario: Navigating to the forgotten password page
    When I click on the "Forgotten Password" link
    Then I should be redirected to the password reset page
```

## 🏗 **Test Execution**
### 1️⃣ **Run tests using Maven**
```sh
mvn test
```
### 2️⃣ **Run specific tests using TestNG**
```sh
mvn test -DsuiteXmlFile=testng.xml
```
### 3️⃣ **Run Parallel Execution (TestNG)**
Modify `testng.xml`:
```xml
<suite name="Cucumber Test Suite" parallel="classes" thread-count="2">
    <test name="Cucumber Tests">
        <classes>
            <class name="runner.TestRunner"/>
        </classes>
    </test>
</suite>
```

## 📜 **Test Runner (Parallel Execution with Cucumber)**
```java
package runner;

import io.cucumber.testng.AbstractTestNGCucumberTests;
import io.cucumber.testng.CucumberOptions;
import org.testng.annotations.DataProvider;

@CucumberOptions(features = "src/test/resources/features",
        glue={"com.opencart.stepDefinitions"},
        plugin={"pretty","html:target/cucumber-reports", "json:target/cucumber.json"},
        monochrome = true,
        publish = true)

public class TestRunner extends AbstractTestNGCucumberTests {
    @Override
    @DataProvider(parallel = true)
    public Object[][] scenarios() {  
        return super.scenarios();  
    }
}
```

## 📊 **Reporting**
- **Cucumber HTML Reports** (`target/cucumber-reports`)
- **Cucumber JSON Reports** (`target/cucumber.json`)

## 🚀 **Next Steps**
- Add **Cross-browser Testing** (Chrome, Firefox, Edge)
- Integrate with **Jenkins for CI/CD**
- Use **Allure Reports** for better reporting

---
#### **Happy Testing! 🎯**
