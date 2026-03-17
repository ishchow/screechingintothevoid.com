## ADDED Requirements

### Requirement: Quarto project configuration
The project SHALL be configured as a Quarto website with blog support via `_quarto.yml` at the project root. The output directory SHALL be `_site`.

#### Scenario: Project renders successfully
- **WHEN** `quarto render` is executed in the project root
- **THEN** the site is rendered to the `_site/` directory without errors

### Requirement: Flatly/darkly theme toggle
The site SHALL use the flatly Bootswatch theme for light mode and the darkly Bootswatch theme for dark mode. Quarto SHALL render a theme toggle control in the navbar.

#### Scenario: Theme toggle is present
- **WHEN** a user visits any page on the site
- **THEN** a light/dark theme toggle icon is visible in the navbar

#### Scenario: Default theme respects system preference
- **WHEN** a user visits the site with a system dark mode preference
- **THEN** the site renders in darkly theme

### Requirement: Top navbar navigation
The site SHALL display a top navigation bar with the site title on the left, and About page link, search, and theme toggle on the right. There SHALL be no sidebar navigation.

#### Scenario: Navbar layout
- **WHEN** a user visits any page
- **THEN** the navbar displays the blog title on the left and About link, search box, and theme toggle on the right

#### Scenario: No sidebar
- **WHEN** a user visits any page
- **THEN** no sidebar navigation is rendered

### Requirement: Blog listing page
The `index.qmd` at the project root SHALL be a listing page that displays all posts from `posts/**/index.qmd` sorted by date descending. Categories SHALL be enabled.

#### Scenario: Posts are listed
- **WHEN** a user visits the home page
- **THEN** all published (non-draft) posts are listed in reverse chronological order with title, date, description, and categories

#### Scenario: Recursive post discovery
- **WHEN** posts exist in nested year/sequence directories under `posts/`
- **THEN** the listing page discovers and displays all of them

### Requirement: About page
The project SHALL include an `about.qmd` page accessible from the navbar.

#### Scenario: About page renders
- **WHEN** a user clicks "About" in the navbar
- **THEN** the about page is displayed

### Requirement: RSS feed
The blog SHALL generate an RSS feed at `index.xml`.

#### Scenario: RSS feed is generated
- **WHEN** the site is rendered
- **THEN** an RSS feed file is generated and accessible at `/index.xml`

### Requirement: Custom CSS file
The project SHALL include a `styles.css` file for custom style overrides, referenced in `_quarto.yml`.

#### Scenario: Custom styles are applied
- **WHEN** the site is rendered
- **THEN** the `styles.css` file is included in all pages
