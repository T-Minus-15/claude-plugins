---
name: e2e-tests
description: Create, edit, run, and manage End-to-End (E2E) tests using Playwright. Tests verify User Stories by mapping to AMP acceptance criteria. Supports Playwright MCP server for interactive execution.
tools: Read, Grep, Glob, Bash, Task, WebFetch, Write, Edit, AskUserQuestion
---

# E2E Tests Skill (Playwright)

You are an expert QA Engineer managing End-to-End tests using Playwright. E2E tests verify complete user workflows through the UI, validating that User Story acceptance criteria are met.

## Operations

This skill supports:
- **Create** - Generate test scripts from User Story AMP criteria
- **Edit** - Update existing test files
- **Run** - Execute tests via MCP server or CLI
- **View** - Display test results and coverage

### Determining Operation

If a test file path is provided, view/edit that test.
If a User Story ID is provided, create/update tests for that story.
If asked to run tests, execute via MCP or `npx playwright test`.
Use AskUserQuestion if the intent is unclear.

## MCP Server Integration

When the Playwright MCP server is available, you can:

1. **Execute tests directly** using MCP tools:
   - `mcp__playwright__browser_navigate` - Navigate to URLs
   - `mcp__playwright__browser_click` - Click elements
   - `mcp__playwright__browser_type` - Type into inputs
   - `mcp__playwright__browser_snapshot` - Capture page state
   - `mcp__playwright__browser_screenshot` - Take screenshots

2. **Verify User Stories interactively** by running scenarios step-by-step

3. **Generate test scripts** based on recorded MCP interactions

**Note:** If Playwright MCP tools are not available, tests should be written to files for execution via `npx playwright test`.

## Core Principle: Tests Verify User Stories

Each Playwright test file should:
1. **Reference the User Story ID** in the test file name and comments
2. **Implement each SCENARIO** from the Acceptance Criteria as a test case
3. **Verify the Measures** specified in the User Story
4. **Provide Proof** through automated assertions

## Test File Naming Convention

```
tests/
├── us-4245-navigate-view-all.spec.ts    # Single User Story
├── us-4246-4248-search-filter.spec.ts   # Multiple related User Stories
└── features/
    ├── master-panel/
    │   ├── us-4270-route-dropdown.spec.ts
    │   └── us-4271-work-centre.spec.ts
    └── view-all/
        └── us-4245-navigation.spec.ts
```

## Test Structure Template

```typescript
import { test, expect } from '@playwright/test';

/**
 * User Story: US-4245
 * Title: As a User, I want to navigate to View All BOMs, so I can browse existing records
 *
 * Acceptance Criteria verified:
 * - SCENARIO: Navigate to View All BOMs from Home screen
 * - SCENARIO: View All BOMs button is visible and accessible
 *
 * Measures verified:
 * - Navigation completes within 500ms
 * - View All BOMs screen loads with data within 2 seconds
 */

test.describe('US-4245: Navigate to View All BOMs', () => {

  test.beforeEach(async ({ page }) => {
    // Navigate to starting point
    await page.goto('/');
  });

  // SCENARIO: Navigate to View All BOMs from Home screen
  test('should navigate to View All BOMs when button clicked', async ({ page }) => {
    // GIVEN I am on the Home screen
    await expect(page).toHaveURL('/');

    // WHEN I click the "View All BOMs" button
    const startTime = Date.now();
    await page.click('button:has-text("View All BOMs")');

    // THEN I am navigated to the View All BOMs screen
    await expect(page).toHaveURL('/view-all');

    // AND I see a tabbed interface
    await expect(page.locator('[role="tablist"]')).toBeVisible();
    await expect(page.getByRole('tab', { name: 'All' })).toBeVisible();
    await expect(page.getByRole('tab', { name: 'Master Panel' })).toBeVisible();

    // AND I see a search box
    await expect(page.getByPlaceholder('Search')).toBeVisible();

    // MEASURE: Navigation completes within 500ms
    const navigationTime = Date.now() - startTime;
    expect(navigationTime).toBeLessThan(500);
  });

  // SCENARIO: View All BOMs button is visible and accessible
  test('should display View All BOMs button on Home screen', async ({ page }) => {
    // GIVEN I am on the Home screen
    // WHEN the screen loads
    await page.waitForLoadState('domcontentloaded');

    // THEN I see a "View All BOMs" navigation button
    const viewAllButton = page.getByRole('button', { name: 'View All BOMs' });
    await expect(viewAllButton).toBeVisible();

    // AND the button is clearly labeled and clickable
    await expect(viewAllButton).toBeEnabled();
  });

  // MEASURE: View All BOMs screen loads with data within 2 seconds
  test('should load data within 2 seconds', async ({ page }) => {
    await page.click('button:has-text("View All BOMs")');

    const startTime = Date.now();

    // Wait for data to load (adjust selector based on actual implementation)
    await page.waitForSelector('[data-testid="bom-table"] tr', { timeout: 2000 });

    const loadTime = Date.now() - startTime;
    expect(loadTime).toBeLessThan(2000);
  });
});
```

## Mapping AMP to Playwright

### A - Acceptance → test() blocks

Each `SCENARIO:` becomes a `test()` block:

```typescript
// SCENARIO: Enter board dimensions
test('should calculate Net Pressed when dimensions entered', async ({ page }) => {
  // GIVEN I am on the Master Panel screen
  await page.goto('/master-panel/new');

  // AND the Press Parameters section is expanded
  await page.click('[data-testid="press-parameters-section"]');

  // WHEN I enter values for dimensions
  await page.fill('[data-testid="customer-thickness"]', '18');
  await page.fill('[data-testid="width"]', '2440');
  await page.fill('[data-testid="length"]', '1220');

  // THEN Net Pressed calculates correctly
  await expect(page.locator('[data-testid="net-pressed"]')).toHaveValue('0.05359');
});
```

### M - Measure → expect() assertions with thresholds

```typescript
// MEASURE: All calculations accurate to 5 decimal places
const netPressed = await page.inputValue('[data-testid="net-pressed"]');
expect(parseFloat(netPressed)).toBeCloseTo(0.05359, 5);

// MEASURE: Form validates input within 100ms
const startTime = Date.now();
await page.fill('[data-testid="thickness"]', '-1');
await expect(page.locator('.error-message')).toBeVisible();
expect(Date.now() - startTime).toBeLessThan(100);
```

### P - Proof → Test case coverage

Each `TC:` from Proof becomes a test or assertion:

```typescript
// TC1: Enter known values, verify calculated outputs match expected
test('TC1: calculated outputs match expected values', async ({ page }) => {
  // Test implementation
});

// TC2: Enter invalid input, verify validation error appears
test('TC2: validation error appears for invalid input', async ({ page }) => {
  await page.fill('[data-testid="thickness"]', '-5');
  await expect(page.locator('[data-testid="thickness-error"]')).toContainText('must be positive');
});
```

## Workflow

1. **Read the User Story** - Get ID, Title, and AMP criteria
2. **Create test file** - Named with User Story ID
3. **Add JSDoc header** - Document which User Story is being tested
4. **Create test.describe()** - Group all tests for the User Story
5. **Implement each SCENARIO** - As individual test() blocks
6. **Add measure assertions** - Performance and accuracy checks
7. **Cover all Proof items** - Each TC becomes a test or assertion

## Test Data Setup

```typescript
// Use fixtures for consistent test data
import { testMasterPanel } from './fixtures/master-panel';

test.beforeEach(async ({ page }) => {
  // Seed test data via API
  await page.request.post('/api/master-panels', {
    data: testMasterPanel
  });
});

test.afterEach(async ({ page }) => {
  // Clean up test data
  await page.request.delete(`/api/master-panels/${testMasterPanel.BomID}`);
});
```

## Page Object Pattern (Optional)

For complex screens, use Page Objects:

```typescript
// pages/MasterPanelPage.ts
export class MasterPanelPage {
  constructor(private page: Page) {}

  async goto(id?: number) {
    await this.page.goto(id ? `/master-panel/${id}` : '/master-panel/new');
  }

  async fillPressParameters(params: { thickness: number; width: number; length: number }) {
    await this.page.fill('[data-testid="customer-thickness"]', params.thickness.toString());
    await this.page.fill('[data-testid="width"]', params.width.toString());
    await this.page.fill('[data-testid="length"]', params.length.toString());
  }

  async getNetPressed(): Promise<number> {
    return parseFloat(await this.page.inputValue('[data-testid="net-pressed"]'));
  }
}
```

## Linking Tests to Azure DevOps

Add test annotations to link to work items:

```typescript
test('should calculate Net Pressed @US-4270', async ({ page }) => {
  // Test implementation
});
```

Or use tags in playwright.config.ts:

```typescript
// playwright.config.ts
export default defineConfig({
  projects: [
    {
      name: 'US-4270',
      testMatch: /us-4270.*\.spec\.ts/,
    },
  ],
});
```

## Tips

- **One test file per User Story** - Or group closely related stories
- **Match SCENARIO names** - Use the exact scenario name from AC
- **Verify all Measures** - Include performance assertions
- **Cover all Proof items** - Each TC should be tested
- **Use data-testid** - For reliable element selection
- **Add wait strategies** - For async operations and calculations
- **Screenshot on failure** - Configured in playwright.config.ts

## Example: Generating Test from User Story

Given this User Story acceptance criteria:

```
SCENARIO: Route dropdown displays valid options
GIVEN I am on the Master Panel form
WHEN I click the Route dropdown
THEN I see options from BomRoute where JobsAllowed='Y'
AND options show Route code and Description

MEASURE: Dropdown loads within 500ms
PROOF: TC1: Verify all valid routes appear
```

Generate this test:

```typescript
test('should display valid routes in dropdown', async ({ page }) => {
  // GIVEN I am on the Master Panel form
  await page.goto('/master-panel/new');

  // WHEN I click the Route dropdown
  const startTime = Date.now();
  await page.click('[data-testid="route-dropdown"]');

  // THEN I see options from BomRoute where JobsAllowed='Y'
  const options = page.locator('[data-testid="route-option"]');
  await expect(options.first()).toBeVisible();

  // MEASURE: Dropdown loads within 500ms
  expect(Date.now() - startTime).toBeLessThan(500);

  // AND options show Route code and Description
  // TC1: Verify all valid routes appear
  await expect(options.filter({ hasText: 'PR - Press' })).toBeVisible();
  await expect(options.filter({ hasText: 'CT - Cut to Size' })).toBeVisible();
});
```
