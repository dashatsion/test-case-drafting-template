# Gold-Standard Test Case Examples

The quality bar: a tester who has never seen the feature can run each case top to bottom and know exactly what "pass" means using only what is written.

These examples are product-agnostic. Replace example wording, roles, fields, and page names with the actual source of truth for your product.

---

## List page — pagination

Verify a list page supports pagination

### Permission
Admin or authorized user.

### Preconditions
1. User is logged in.
2. User has access to the feature.
3. More than 10 records exist so pagination is active.
4. The feature list page is open.

### Steps
1. Observe the list of records
  ***Expected result***:
  A list of records is displayed.
  Each row shows the key fields defined by the product spec.

2. Scroll to the pagination control at the bottom of the list
  ***Expected result***:
  Pagination controls are visible.
  The first page is selected.

3. Click the next page control
  ***Expected result***:
  The list updates to show the next set of records.
  The pagination state updates to the next page.

4. Click the previous page control
  ***Expected result***:
  The list returns to the previous set of records.
  The pagination state updates to the previous page.

---

## Create flow — required fields

Create an item with required fields

### Permission
Admin or authorized user.

### Preconditions
1. User is logged in.
2. User has access to the feature.
3. The feature list page is open.

### Steps
1. Click the create button
  ***Expected result***:
  The create form or modal opens.
  Required fields are visible.

2. Enter valid values into all required fields
  ***Expected result***:
  The values are accepted.
  No validation errors are shown.

3. Save the item
  ***Expected result***:
  The form or modal closes.
  A success confirmation is shown if supported.
  The created item appears in the list.

4. Open the created item
  ***Expected result***:
  The detail page or view state opens.
  The displayed values match the values entered during creation.

---

## Settings flow — change frequency

Change an item's frequency setting and verify the visible schedule updates

### Permission
Admin or authorized user.

### Preconditions
1. User is logged in.
2. User has access to the feature.
3. An item with an existing frequency setting exists.
4. The item detail page is open.

### Steps
1. Observe the current frequency or schedule
  ***Expected result***:
  The current frequency is displayed.
  Related schedule or period information matches the current frequency.

2. Open the item settings
  ***Expected result***:
  Settings are displayed.
  The current frequency value is selected.

3. Change the frequency to another valid value
  ***Expected result***:
  The new frequency value is selected.

4. Save the change
  ***Expected result***:
  The settings are saved.
  The visible schedule or period information updates to match the new frequency.

---

## Recurring flow — carry forward unfinished item

Verify an unfinished item carries forward to the next occurrence

### Permission
Admin or authorized user.

### Preconditions
1. User is logged in.
2. User has access to the feature.
3. A recurring series exists.
4. The current occurrence has one unfinished item.

### Steps
1. Complete or close the current occurrence without finishing the item
  ***Expected result***:
  The current occurrence is completed or closed.
  The item remains unfinished.

2. Open the next occurrence in the series
  ***Expected result***:
  The unfinished item appears in the next occurrence.

3. Review the carried-forward item details
  ***Expected result***:
  The carried-forward item keeps the expected details from the previous occurrence.

4. Mark the item complete
  ***Expected result***:
  The item is marked complete in the current occurrence.
  Previous occurrences are not unexpectedly changed.