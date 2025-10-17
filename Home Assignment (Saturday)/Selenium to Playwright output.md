/**
 * Playwright TypeScript Test Suite for Formy Project – Complete Web Form
 * 
 * Author: Harish
 * Date: 05/04/2025
 * 
 * Description:
 * This test suite validates the "Complete Web Form" functionality on the Formy demo site
 * using Playwright with TypeScript. It covers form field population (text, radio, checkbox,
 * dropdown, date picker), submission, and post-submission verification.
 * 
 * Playwright best practices applied:
 * - Auto-waiting via built-in Playwright locators
 * - Page object model not used here for simplicity (inline locators)
 * - Proper test isolation using test fixtures
 * - No manual waits; leveraging Playwright's auto-waiting and assertions
 * - Exception handling via Playwright's built-in error reporting
 */

import { test, expect } from '@playwright/test';

const BASE_URL = 'https://formy-project.herokuapp.com';

test.describe('Complete Web Form Tests', () => {

  test.beforeEach(async ({ page }) => {
    // Navigate to the form page before each test
    await page.goto(`${BASE_URL}/form`);
  });

  /**
   * Test 1 – Fill all fields (text, radio, checkbox, dropdown, date) and submit.
   * Verifies that the user is redirected to the thank-you page.
   */
  test('Complete the form and verify successful submission', async ({ page }) => {
    // ----------- TEXT FIELDS ------------
    await page.locator('#first-name').fill('John');
    await page.locator('#last-name').fill('Doe');
    await page.locator('#job-title').fill('Automation Engineer');

    // ----------- RADIO BUTTONS ----------
    // Select "College"
    await page.locator('#radio-button-2').check();

    // ----------- CHECKBOXES -------------
    // Select "Male" and "Prefer not to say"
    await page.locator('#checkbox-1').check();
    await page.locator('#checkbox-3').check();

    // ----------- DROPDOWN (SELECT) -------
    const selectMenu = page.locator('#select-menu');
    await selectMenu.selectOption({ label: '2-4' }); // choose 2–4 years

    // ----------- DATE PICKER ------------
    const dateInput = page.locator('#datepicker');
    await dateInput.fill('10/20/2025'); // mm/dd/yyyy format

    // ----------- SUBMIT -----------------
    // The submit button is an <a> tag – click it directly
    await page.locator('a.btn.btn-lg.btn-primary').click();

    // ----------- VERIFICATION ------------
    // Wait for navigation to /thanks and assert URL
    await page.waitForURL(/\/thanks$/);
    const currentUrl = page.url();
    expect(currentUrl).toMatch(/\/thanks$/);
  });

  /**
   * Test 2 – Verify each radio button can be selected individually.
   */
  test('Select each education level radio button and assert state', async ({ page }) => {
    const highSchool = page.locator('#radio-button-1');
    const college = page.locator('#radio-button-2');
    const gradSchool = page.locator('#radio-button-3');

    // High School
    await highSchool.check();
    await expect(highSchool).toBeChecked();

    // College
    await college.check();
    await expect(college).toBeChecked();
    await expect(highSchool).not.toBeChecked();

    // Grad School
    await gradSchool.check();
    await expect(gradSchool).toBeChecked();
    await expect(college).not.toBeChecked();
  });

  /**
   * Test 3 – Validate dropdown options and date-picker behaviour.
   */
  test('Check dropdown values and date picker input', async ({ page }) => {
    const expectedOptions = ['Select an option', '0-1', '2-4', '5-9', '10+'];
    const selectMenu = page.locator('#select-menu');

    // Verify all dropdown options are present
    const actualOptions = await selectMenu.locator('option').allTextContents();
    expect(actualOptions).toEqual(expectedOptions);

    // Select each option sequentially and verify
    for (let i = 1; i < expectedOptions.length; i++) {
      await selectMenu.selectOption({ index: i });
      const selectedOption = await selectMenu.locator('option:checked').textContent();
      expect(selectedOption?.trim()).toBe(expectedOptions[i]);
    }

    // ----------- DATE PICKER VALIDATION ------------
    const dateField = page.locator('#datepicker');
    await dateField.fill('12/31/2025');

    // Verify the entered date is correctly reflected
    await expect(dateField).toHaveValue('12/31/2025');
  });
});


------------------------------------------------------------
Notes:

Playwright Version: Compatible with Playwright v1.40+ (latest as of 2025).
Auto-waiting: Playwright automatically waits for elements to be actionable (visible, enabled, etc.), so explicit waits like WebDriverWait are unnecessary.
Assertions: Uses expect from @playwright/test for built-in retry-ability and clear error messages.
Date Format: Assumes the date input expects mm/dd/yyyy, consistent with the original Selenium test.
Cleanup: Playwright handles browser lifecycle automatically via test fixtures—no need for manual tearDown.


Make sure to install dependencies:
npm init playwright@latest

And run tests with:
npx playwright test