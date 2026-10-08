# Selenium XPath Automation

## Overview

This demonstrates **Selenium WebDriver automation using XPath** in Python.

This covers different XPath concepts such as:

- Attribute XPath
- `text()`
- `contains()`
- `starts-with()`
- `and`
- `or`
- Parent
- Ancestor
- Child
- Following
- XPath Index
- Explicit Wait
- `find_elements()`
- Dropdown handling
- Checkbox handling
- Radio button handling
- Submit button handling

The purpose is to understand how XPath can be used to locate and interact with web elements during automation testing.

---

## Objective

The main objective is to practice Selenium WebDriver with different XPath techniques and understand how web elements can be located in the HTML DOM.

This follows a real-time student registration automation scenario.

### Automation Flow

```text
Open Registration Page
        ↓
Enter Username
        ↓
Enter Password
        ↓
Enter Additional Information
        ↓
Select Dropdown
        ↓
Select Checkbox
        ↓
Select Radio Button
        ↓
Click Submit
        ↓
Verify Submission
```

### code
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import Select, WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time


# =========================================================
# START BROWSER
# =========================================================

driver = webdriver.Chrome()
driver.maximize_window()

wait = WebDriverWait(driver, 10)


try:

    # =====================================================
    # TC01 - Open Registration Page
    # Concept: get()
    # =====================================================

    print("\nTC01 - OPEN REGISTRATION PAGE")

    driver.get("https://www.selenium.dev/selenium/web/web-form.html")

    print("Registration page opened successfully")


    # =====================================================
    # TC02 - Locate Username
    # Concept: Attribute XPath
    # =====================================================

    print("\nTC02 - LOCATE USERNAME")

    username = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']"
    )

    print("Username textbox found")

    username.send_keys("Sarisha")


    # =====================================================
    # TC03 - Enter Password
    # Concept: Attribute XPath
    # =====================================================

    print("\nTC03 - ENTER PASSWORD")

    password = driver.find_element(
        By.XPATH,
        "//input[@name='my-password']"
    )

    print("Password textbox found")

    password.send_keys("12345")


    # =====================================================
    # TC04 - Locate Submit
    # Concept: text()
    # =====================================================

    print("\nTC04 - LOCATE SUBMIT")

    submit_button = driver.find_element(
        By.XPATH,
        "//button[text()='Submit']"
    )

    print("Submit button found")


    # =====================================================
    # TC05 - Locate Textbox Dynamically
    # Concept: contains()
    # =====================================================

    print("\nTC05 - CONTAINS()")

    text_box = driver.find_element(
        By.XPATH,
        "//input[contains(@name,'my-text')]"
    )

    print("Textbox located using contains()")


    # =====================================================
    # TC06 - Locate Element With Prefix
    # Concept: starts-with()
    # =====================================================

    print("\nTC06 - STARTS-WITH()")

    prefix_element = driver.find_element(
        By.XPATH,
        "//input[starts-with(@name,'my-')]"
    )

    print("Element located using starts-with()")


    # =====================================================
    # TC07 - Find Input Using Two Attributes
    # Concept: and
    # =====================================================

    print("\nTC07 - AND")

    username_two_attributes = driver.find_element(
        By.XPATH,
        "//input[@name='my-text' and @type='text']"
    )

    print("Element found using two attributes")


    # =====================================================
    # TC08 - Find Element Using Alternatives
    # Concept: or
    # =====================================================

    print("\nTC08 - OR")

    alternative_element = driver.find_element(
        By.XPATH,
        "//input[@name='my-text' or @name='my-password']"
    )

    print("Element found using OR")


    # =====================================================
    # TC09 - Find Parent
    # Concept: parent
    # =====================================================

    print("\nTC09 - PARENT")

    parent_element = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']/parent::*"
    )

    print("Parent element found")

    print("Parent tag:", parent_element.tag_name)


    # =====================================================
    # TC10 - Find Form From Input
    # Concept: ancestor
    # =====================================================

    print("\nTC10 - ANCESTOR")

    ancestor_form = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']/ancestor::form"
    )

    print("Ancestor form found")

    print("Form tag:", ancestor_form.tag_name)


    # =====================================================
    # TC11 - Find Child Inputs
    # Concept: child
    # =====================================================

    print("\nTC11 - CHILD")

    child_inputs = driver.find_elements(
        By.XPATH,
        "//form/child::*"
    )

    print("Child elements found:", len(child_inputs))


    # =====================================================
    # TC12 - Find Next Element
    # Concept: following
    # =====================================================

    print("\nTC12 - FOLLOWING")

    following_element = driver.find_element(
        By.XPATH,
        "//input[@name='my-text']/following::*[1]"
    )

    print("Following element found")

    print("Tag:", following_element.tag_name)


    # =====================================================
    # TC13 - Find Checkbox
    # Concept: Attribute XPath
    # =====================================================

    print("\nTC13 - CHECKBOX")

    checkbox = driver.find_element(
        By.XPATH,
        "//input[@type='checkbox']"
    )

    print("Checkbox found")

    if not checkbox.is_selected():

        checkbox.click()

    print("Checkbox selected:", checkbox.is_selected())


    # =====================================================
    # TC14 - Find Radio Button
    # Concept: Attribute XPath
    # =====================================================

    print("\nTC14 - RADIO BUTTON")

    radio_button = driver.find_element(
        By.XPATH,
        "//input[@type='radio']"
    )

    print("Radio button found")

    if not radio_button.is_selected():

        radio_button.click()

    print("Radio selected:", radio_button.is_selected())


    # =====================================================
    # TC15 - Select Dropdown
    # Concept: XPath + Select
    # =====================================================

    print("\nTC15 - DROPDOWN")

    dropdown_element = driver.find_element(
        By.XPATH,
        "//select"
    )

    dropdown = Select(dropdown_element)

    dropdown.select_by_index(1)

    print("Dropdown option selected")


    # =====================================================
    # TC16 - Find Second Textbox
    # Concept: XPath Index
    # =====================================================

    print("\nTC16 - SECOND TEXTBOX")

    all_textboxes = driver.find_elements(
        By.XPATH,
        "//input[@type='text']"
    )

    if len(all_textboxes) >= 2:

        second_textbox = all_textboxes[1]

        print("Second textbox found")

        print(
            "Tag:",
            second_textbox.tag_name
        )

        print(
            "Name:",
            second_textbox.get_attribute("name")
        )

        print(
            "Displayed:",
            second_textbox.is_displayed()
        )

        print(
            "Enabled:",
            second_textbox.is_enabled()
        )

    else:

        print("Second textbox not available")


    # =====================================================
    # TC17 - Verify Submitted Message
    # Concept: text()
    # =====================================================

    print("\nTC17 - VERIFY MESSAGE")

    submit_button = wait.until(
        EC.element_to_be_clickable(
            (
                By.XPATH,
                "//button[text()='Submit']"
            )
        )
    )

    print("Submit button is available")

    print("Submit button is clickable")


    # =====================================================
    # TC18 - Find All Input Fields
    # Concept: find_elements()
    # =====================================================

    print("\nTC18 - FIND ALL INPUT FIELDS")

    inputs = driver.find_elements(
        By.XPATH,
        "//input"
    )

    print(
        "Total input fields:",
        len(inputs)
    )

    for i, element in enumerate(inputs, start=1):

        print(
            "Input",
            i,
            "- Type:",
            element.get_attribute("type"),
            "- Name:",
            element.get_attribute("name")
        )


    # =====================================================
    # TC19 - Find Dynamic Element
    # Concept: contains()
    # =====================================================

    print("\nTC19 - DYNAMIC ELEMENT")

    dynamic_element = driver.find_element(
        By.XPATH,
        "//*[contains(@name,'my-')]"
    )

    print("Dynamic element found")

    print(
        "Tag:",
        dynamic_element.tag_name
    )


    # =====================================================
    # TC20 - COMPLETE AUTOMATION
    # Concept: Multiple XPath Concepts
    # =====================================================

    print("\nTC20 - COMPLETE REGISTRATION AUTOMATION")


    # -----------------------------------------------------
    # Username
    # -----------------------------------------------------

    username = wait.until(
        EC.visibility_of_element_located(
            (
                By.XPATH,
                "//input[@name='my-text']"
            )
        )
    )

    username.clear()

    username.send_keys("Sarisha")

    print("Username entered")


    # -----------------------------------------------------
    # Password
    # -----------------------------------------------------

    password = wait.until(
        EC.visibility_of_element_located(
            (
                By.XPATH,
                "//input[@name='my-password']"
            )
        )
    )

    password.clear()

    password.send_keys("Sarisha@123")

    print("Password entered")


    # -----------------------------------------------------
    # Additional Information
    # -----------------------------------------------------

    textarea = wait.until(
        EC.visibility_of_element_located(
            (
                By.XPATH,
                "//textarea[@name='my-textarea']"
            )
        )
    )

    textarea.send_keys(
        "B.Tech CSE AI ML Student"
    )

    print("Additional information entered")


    # -----------------------------------------------------
    # Checkbox
    # -----------------------------------------------------

    checkbox = driver.find_element(
        By.XPATH,
        "//input[@type='checkbox']"
    )

    if not checkbox.is_selected():

        checkbox.click()

    print("Checkbox selected")


    # -----------------------------------------------------
    # Radio Button
    # -----------------------------------------------------

    radio = driver.find_element(
        By.XPATH,
        "//input[@type='radio']"
    )

    if not radio.is_selected():

        radio.click()

    print("Radio button selected")


    # -----------------------------------------------------
    # Dropdown
    # -----------------------------------------------------

    select_element = driver.find_element(
        By.XPATH,
        "//select"
    )

    select = Select(select_element)

    select.select_by_index(1)

    print("Dropdown selected")


    # -----------------------------------------------------
    # Submit
    # -----------------------------------------------------

    submit = wait.until(
        EC.element_to_be_clickable(
            (
                By.XPATH,
                "//button[text()='Submit']"
            )
        )
    )

    submit.click()

    print("Submit button clicked")


    # -----------------------------------------------------
    # Verify Submission
    # -----------------------------------------------------

    time.sleep(2)

    print("Registration automation completed")


    # =====================================================
    # FINAL RESULT
    # =====================================================

    print("\n========================================")

    print("ALL TEST CASES EXECUTED")

    print("TC01 to TC20 completed")

    print("========================================")


except Exception as e:

    print("\n========================================")

    print("ERROR OCCURRED:")

    print(e)

    print("========================================")


finally:

    input("\nPress Enter to close browser...")

    driver.quit()
```

### Output
<img width="1916" height="1067" alt="image" src="https://github.com/user-attachments/assets/a9b864ed-88de-4fca-a070-ca9834ee4f0c" />
<img width="1882" height="983" alt="image" src="https://github.com/user-attachments/assets/faf4437f-d359-424b-84f1-110187225000" />
<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/ba31e24d-b687-4f44-925f-43b0d7829085" />
<img width="1916" height="1067" alt="image" src="https://github.com/user-attachments/assets/3b763772-bfbb-494d-a964-55f49e0be9c0" />

### github link
https://github.com/Sarishatheiveegan/Selenium-XPath-Automation_.git
