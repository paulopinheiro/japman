# UC-02 — Search Plugins

## Goal

Allow the Audio Engineer to search and consult plugins registered in the Plugin Catalog using multiple search criteria, inspect plugin information, and access plugin maintenance.

## Primary Actor

Audio Engineer

## Preconditions

- The Plugin Catalog is available.

## Postconditions

- The search results reflect the criteria specified by the user.
- No changes are made to the Plugin Catalog by this use case.

## Trigger

The Audio Engineer requests access to the plugin search function.

## Main Flow

1. The system displays the Search Plugins screen.
2. The system initializes all search criteria without restrictions, so that all cataloged plugins are included.
3. The system displays the matching plugins in a tabular format.
4. The Audio Engineer modifies one or more search criteria.
5. The system automatically updates the search results after the user stops modifying the criteria for a short interval.
6. The Audio Engineer may change the sorting criterion by selecting the corresponding column header.
7. The system sorts the results according to the selected column, in ascending or descending order.
8. The Audio Engineer may select a plugin to inspect its details.
9. The system displays the selected plugin's detailed information.
10. The Audio Engineer may double-click a plugin in the results table to access the Maintain Plugin Registry use case.
11. The system opens Maintain Plugin Registry with the selected plugin identified.

## Alternative Flows

### A1 — No Matching Plugins

At step 5:

1. If no plugins match the specified criteria, the system displays an empty results table.
2. The system displays the message "No plugins found".
3. The use case remains available for further searches.

### A2 — Clear Search Criteria

At any time while using the search screen:

1. The Audio Engineer requests that all search criteria be cleared.
2. The system removes all search restrictions.
3. The system displays all plugins registered in the Plugin Catalog.
4. The current sorting criterion and direction remain unchanged.

## Business Rules

### BR-01 — Combined Search Criteria

When multiple search criteria are specified, a plugin must satisfy all specified criteria to be included in the search results.

Criteria that are not specified must not restrict the search results.

### BR-02 — Plugin Name Pattern

The system must allow the Audio Engineer to search for plugins using name patterns, including wildcard characters.

The wildcard syntax is not defined by this use case.

### BR-03 — Search Criteria

The system must support the following search criteria:

- Plugin Name Pattern
- Manufacturer
- Category
- Subcategory
- Emulated Equipment
- Tags
- Plugin Format
- Platform
- Catalog Date

### BR-04 — Platform Selection

The Platform criterion must allow any combination of the following options:

- Linux Native
- Windows via yabridge

When no platform restriction is specified, plugins from all supported platforms must be included.

### BR-05 — Catalog Date

The Catalog Date criterion must allow the Audio Engineer to restrict results to plugins cataloged within a user-specified number of days.

When no period is specified, no date restriction must be applied.

The catalog date represents the date on which JAPMan first registered the plugin, not the operating system's file installation date.

### BR-06 — Automatic Search Update

Search results must be updated automatically after the Audio Engineer stops modifying the search criteria for a short interval.

The exact interval and implementation mechanism are outside the scope of this use case.

### BR-07 — Search Results Presentation

Search results must be presented in tabular format.

The table must display available plugin information, including the plugin version whenever that information is available.

### BR-08 — Result Sorting

The Audio Engineer must be able to sort search results by available data columns.

Sorting must support both ascending and descending order.

The sorting criterion and direction must be independent of the search criteria. Changing or clearing search criteria must not alter the current sorting configuration.

### BR-09 — Clear Search Criteria

The system must provide a single action to clear all search criteria and restore the initial search state, displaying all plugins registered in the Plugin Catalog.

Clearing search criteria must not alter the current sorting configuration.

### BR-10 — Search State Reset

Whenever the Audio Engineer leaves the Search Plugins screen, the current search criteria and sorting configuration must be discarded.

When the screen is accessed again, the system must restore the initial search state:

- No search restrictions.
- All cataloged plugins included in the results.
- Default sorting configuration.

### BR-11 — Plugin Details

The Audio Engineer must be able to inspect detailed information about a selected plugin.

The detailed view is intended for consultation and does not provide plugin registry maintenance operations.

### BR-12 — Access to Plugin Maintenance

The Audio Engineer must be able to access the Maintain Plugin Registry use case by double-clicking a plugin in the search results.

The selected plugin must be identified when the maintenance use case is opened.

Maintain Plugin Registry must also be accessible independently of Search Plugins.