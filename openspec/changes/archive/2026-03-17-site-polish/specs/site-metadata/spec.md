## ADDED Requirements

### Requirement: Open Graph metadata enabled
The site SHALL set `open-graph: true` in `_quarto.yml` under the `website` key.

#### Scenario: Open Graph meta tags generated
- **WHEN** a page is rendered
- **THEN** the HTML head contains `og:title`, `og:description`, and `og:site_name` meta tags auto-populated from page metadata

### Requirement: Twitter Card metadata enabled
The site SHALL set `twitter-card: true` in `_quarto.yml` under the `website` key.

#### Scenario: Twitter Card meta tags generated
- **WHEN** a page is rendered
- **THEN** the HTML head contains `twitter:title`, `twitter:description`, and `twitter:card` meta tags auto-populated from page metadata

### Requirement: Footer displays real-name copyright
The page footer center section SHALL display "© 2026 Ishaat Chowdhury".

#### Scenario: Copyright text
- **WHEN** a visitor scrolls to the page footer
- **THEN** the center of the footer reads "© 2026 Ishaat Chowdhury"

### Requirement: Footer displays GitHub source link
The page footer right section SHALL display a GitHub icon linking to `https://github.com/ishchow/screechingintothevoid.com` with an `aria-label` of "Source Code".

#### Scenario: GitHub icon in footer
- **WHEN** a visitor views the page footer
- **THEN** a GitHub icon is visible on the right side of the footer

#### Scenario: GitHub link target
- **WHEN** a visitor clicks the GitHub icon in the footer
- **THEN** they are navigated to `https://github.com/ishchow/screechingintothevoid.com`
