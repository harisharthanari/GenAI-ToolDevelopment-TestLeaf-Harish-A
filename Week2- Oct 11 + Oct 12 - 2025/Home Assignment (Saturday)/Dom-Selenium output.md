/****************************************************************************************
 *  Author : Harish
 *  Date   : 16/10/2025
 *  Description :
 *      Selenium‑Java TestNG script that automates the “Complete Web Form” page.
 *      • Demonstrates filling text fields, selecting radio buttons, checkboxes,
 *        dropdowns and a date picker.
 *      • Uses explicit waits (WebDriverWait) – no Thread.sleep().
 *      • Contains a single class with @BeforeClass/@AfterClass for driver life‑cycle
 *        and three independent @Test methods.
 ****************************************************************************************/

package com.formy.tests;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
import org.testng.annotations.*;

import java.time.Duration;

/**
 * TestNG test class that validates the “Complete Web Form” functionality.
 */
public class CompleteWebFormTest {

    private WebDriver driver;
    private WebDriverWait wait;
    // TODO: replace with the real URL where the form is hosted
    private static final String BASE_URL = "https://formy-project.herokuapp.com";   // example placeholder

    // -------------------------------------------------------------------------
    // --------------------------- Test Setup -----------------------------------
    // -------------------------------------------------------------------------
    @BeforeClass
    public void setUp() {
        // Initialise ChromeDriver (make sure chromedriver executable is on the PATH)
        ChromeOptions options = new ChromeOptions();
        options.addArguments("--start-maximized");          // open browser maximised
        options.addArguments("--disable-infobars");        // hide infobars
        driver = new ChromeDriver(options);

        // Explicit wait – 15 seconds timeout, polling every 500 ms
        wait = new WebDriverWait(driver, Duration.ofSeconds(15));

        // Navigate directly to the form page
        driver.get(BASE_URL + "/form");
    }

    // -------------------------------------------------------------------------
    // -------------------------- Test Tear‑Down ---------------------------------
    // -------------------------------------------------------------------------
    @AfterClass
    public void tearDown() {
        if (driver != null) {
            driver.quit();
        }
    }

    // -------------------------------------------------------------------------
    // -------------------------- Helper Methods ---------------------------------
    // -------------------------------------------------------------------------

    /**
     * Waits for an element to be visible and returns it.
     */
    private WebElement visible(By locator) {
        return wait.until(ExpectedConditions.visibilityOfElementLocated(locator));
    }

    /**
     * Waits for an element to be clickable and returns it.
     */
    private WebElement clickable(By locator) {
        return wait.until(ExpectedConditions.elementToBeClickable(locator));
    }

    // -------------------------------------------------------------------------
    // --------------------------- Test Cases ------------------------------------
    // -------------------------------------------------------------------------

    /**
     * Test 1 – Fill all fields (text, radio, checkbox, dropdown, date) and submit.
     * Verifies that the user is redirected to the thank‑you page.
     */
    @Test(priority = 1, description = "Complete the form and verify successful submission")
    public void testFillFormAndSubmit() {
        // ----------- TEXT FIELDS ------------
        visible(By.id("first-name")).sendKeys("John");
        visible(By.id("last-name")).sendKeys("Doe");
        visible(By.id("job-title")).sendKeys("Automation Engineer");

        // ----------- RADIO BUTTONS ----------
        // Select "College"
        clickable(By.id("radio-button-2")).click();

        // ----------- CHECKBOXES -------------
        // Select "Male" and "Prefer not to say"
        clickable(By.id("checkbox-1")).click();
        clickable(By.id("checkbox-3")).click();

        // ----------- DROPDOWN (SELECT) -------
        Select experienceSelect = new Select(visible(By.id("select-menu")));
        experienceSelect.selectByVisibleText("2-4");   // choose 2‑4 years

        // ----------- DATE PICKER ------------
        WebElement dateInput = visible(By.id("datepicker"));
        // Clear any pre‑filled value and type the date in the required format
        dateInput.clear();
        dateInput.sendKeys("10/20/2025");   // mm/dd/yyyy

        // ----------- SUBMIT -----------------
        // The submit button is an <a> tag – click it directly
        clickable(By.cssSelector("a.btn.btn-lg.btn-primary")).click();

        // ----------- VERIFICATION ------------
        // After submission the page should navigate to /thanks
        wait.until(ExpectedConditions.urlContains("/thanks"));
        String currentUrl = driver.getCurrentUrl();
        Assert.assertTrue(currentUrl.endsWith("/thanks"),
                "Expected to be on the thank‑you page, but was on: " + currentUrl);
    }

    /**
     * Test 2 – Verify each radio button can be selected individually.
     */
    @Test(priority = 2, description = "Select each education level radio button and assert state")
    public void testRadioButtonsSelection() {
        // High School
        WebElement highSchool = clickable(By.id("radio-button-1"));
        highSchool.click();
        Assert.assertTrue(highSchool.isSelected(), "High School radio should be selected");

        // College
        WebElement college = clickable(By.id("radio-button-2"));
        college.click();
        Assert.assertTrue(college.isSelected(), "College radio should be selected");
        Assert.assertFalse(highSchool.isSelected(), "High School radio should be deselected");

        // Grad School
        WebElement gradSchool = clickable(By.id("radio-button-3"));
        gradSchool.click();
        Assert.assertTrue(gradSchool.isSelected(), "Grad School radio should be selected");
        Assert.assertFalse(college.isSelected(), "College radio should be deselected");
    }

    /**
     * Test 3 – Validate dropdown options and date‑picker behaviour.
     */
    @Test(priority = 3, description = "Check dropdown values and date picker input")
    public void testDropdownAndDatepicker() {
        // ----------- VERIFY DROPDOWN OPTIONS ----------
        Select expSelect = new Select(visible(By.id("select-menu")));
        // Expected options list
        String[] expected = {"Select an option", "0-1", "2-4", "5-9", "10+"};
        for (int i = 0; i < expected.length; i++) {
            String actual = expSelect.getOptions().get(i).getText().trim();
            Assert.assertEquals(actual, expected[i],
                    "Dropdown option mismatch at index " + i);
        }

        // Choose each option sequentially and verify selection
        for (int i = 1; i < expected.length; i++) { // skip the placeholder
            expSelect.selectByIndex(i);
            String selected = expSelect.getFirstSelectedOption().getText().trim();
            Assert.assertEquals(selected, expected[i],
                    "Selected dropdown value does not match expected");
        }

        // ----------- DATE PICKER VALIDATION ------------
        WebElement dateField = visible(By.id("datepicker"));
        dateField.clear();
        dateField.sendKeys("12/31/2025");

        // Verify the entered date is correctly reflected
        Assert.assertEquals(dateField.getAttribute("value"), "12/31/2025",
                "Date picker value mismatch");
    }
}