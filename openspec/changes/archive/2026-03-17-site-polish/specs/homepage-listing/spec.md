## ADDED Requirements

### Requirement: Homepage title suppressed
The homepage SHALL use `pagetitle` instead of `title` so that no visible heading renders on the page, while the browser tab title is preserved.

#### Scenario: No visible title on homepage
- **WHEN** a visitor loads the homepage
- **THEN** no `<h1>` page title is rendered above the listing

#### Scenario: Browser tab title preserved
- **WHEN** a visitor loads the homepage
- **THEN** the browser tab displays "Screeching Into The Void"

### Requirement: Table-style listing on homepage
The homepage listing SHALL use `type: table` to display posts in a tabular format.

#### Scenario: Table rendering
- **WHEN** a visitor loads the homepage
- **THEN** posts are displayed in a table with column headers

### Requirement: Listing displays only date, title, and reading-time fields
The homepage listing SHALL configure `fields: [date, title, reading-time]` and display no other fields.

#### Scenario: Visible columns
- **WHEN** a visitor views the homepage listing
- **THEN** only the Date, Title, and Reading Time columns are visible

#### Scenario: No description column
- **WHEN** a visitor views the homepage listing
- **THEN** there is no description or author column in the table

### Requirement: Categories disabled on listing
The homepage listing SHALL set `categories: false` to suppress the categories sidebar.

#### Scenario: No categories sidebar
- **WHEN** a visitor loads the homepage
- **THEN** no categories sidebar or filter is displayed

### Requirement: Sort and filter UI disabled
The homepage listing SHALL set `sort-ui: false` and `filter-ui: false`.

#### Scenario: No sort controls
- **WHEN** a visitor loads the homepage
- **THEN** no sort dropdown or clickable column headers for sorting are present

#### Scenario: No filter box
- **WHEN** a visitor loads the homepage
- **THEN** no search/filter input box is displayed above the listing

### Requirement: Table hover enabled
The homepage listing SHALL set `table-hover: true` to highlight rows on mouse hover.

#### Scenario: Row highlight on hover
- **WHEN** a visitor hovers over a table row
- **THEN** the row background is highlighted

### Requirement: Posts sorted by date descending
The homepage listing SHALL maintain `sort: "date desc"` to show newest posts first.

#### Scenario: Newest post first
- **WHEN** multiple posts exist
- **THEN** the most recently dated post appears at the top of the table
