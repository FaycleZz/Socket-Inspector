---
applyTo: 'playwright/**'
---

# Writing Playwright Tests

Test files should have a `.test.ts` extension and should be located in the [tests](../../playwright/tests/) directory.

The [page-models directory](../../playwright/page-models/) contains **Page Models**. Page Models are classes that contain reusable Locators and helper functions that interact with locators. Locators should not be created in test files — they should always be created in a Page Model class.

When creating Locators, avoid using page.locator when possible

Do not modify files in the [test-app directory](../../playwright/test-app/), unless told otherwise.

Before using functions or locators from the HostPageModel or the DevtoolsPanelModel, make sure to call the `bringToFront()` method first. This makes it easier to understand the test recordings because the page the test is interacting with will be visible.

Don't forget to use `await` when using `expect`
