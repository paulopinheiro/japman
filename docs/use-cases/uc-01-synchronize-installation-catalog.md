# UC-01 — Synchronize Installation Catalog

## Goal

Synchronize the JAPMan Installation Catalog with plugin installations
available in the system within the synchronization scope selected by
the user.

The synchronization identifies installations that are new, updated,
or no longer found.

## Primary Actor

User

## Preconditions

- JAPMan is running.
- The Installation Catalog is available.
- At least one supported plugin format is available for selection.

## Trigger

The user starts a synchronization of the Installation Catalog.

## Main Success Scenario

1. The user starts the synchronization.
2. The user selects the plugin formats to be included in the
   synchronization.
3. The user optionally specifies an installation name pattern to
   restrict the synchronization scope.
4. The system discovers installations within the selected scope.
5. The system scans the discovered installations according to their
   respective plugin formats.
6. The system compares the discovered installations with the
   Installation Catalog.
7. The system adds installations that are not present in the catalog
   and classifies them as `New`.
8. The system identifies cataloged installations whose synchronization
   signature has changed and classifies them as `Updated`.
9. The system identifies cataloged installations within the
   synchronization scope that were not found and classifies them as
   `Not Found`.
10. The system updates the Installation Catalog accordingly.
11. The system presents the synchronization results to the user.

## Alternative Flows

### A1 — Synchronization with an Installation Name Pattern

If the user specifies an installation name pattern:

1. The system restricts filesystem discovery to installations matching
   the specified pattern.
2. Installations outside the selected pattern are not included in the
   synchronization.
3. Installations outside the synchronization scope are not evaluated
   for changes or `Not Found` status.
4. The system continues with the main success scenario.

### A2 — Selected Plugin Formats

If the user selects only a subset of the available plugin formats:

1. The system searches only the selected formats.
2. Installations belonging to unselected formats are not included in
   the synchronization.
3. Installations belonging to unselected formats are not evaluated
   for changes or `Not Found` status.
4. The system continues with the main success scenario.

### A3 — Inspect Plugins Found in an Installation

If the user wants to inspect the plugins discovered in an installation:

1. The user selects `Plugin names` for the installation.
2. The system displays the plugin names discovered in that installation
   during the current synchronization.
3. The system does not use the Plugin Catalog as the source for this
   information.
4. The user closes the plugin list and returns to the synchronization
   results.

### A4 — Not Found Installations

If one or more cataloged installations within the synchronization
scope are not found:

1. The system identifies the affected installations as `Not Found`.
2. The system presents the affected installations to the user.
3. The user may choose to keep the installations in the catalog.
4. The user may choose to remove the installations from the catalog.
5. The system removes only the installations explicitly selected for
   removal.

## Exception Flows

### E1 — Invalid Installation Name Pattern

If the specified installation name pattern is invalid:

1. The system informs the user that the pattern is invalid.
2. The system does not perform the synchronization using the invalid
   pattern.
3. The user may correct the pattern or cancel the operation.

### E2 — No Installations Found

If no installations are found within the selected synchronization
scope:

1. The system informs the user that no installations were found.
2. The Installation Catalog is not modified as a result of discovered
   installations.
3. The synchronization is completed.

### E3 — Installation Scan Failure

If an installation cannot be successfully scanned:

1. The system records the scan failure.
2. The system reports the affected installation to the user.
3. The system continues synchronizing other installations whenever
   possible.
4. The failed installation is not treated as successfully discovered
   or updated.

## Postconditions

Upon successful completion:

- Newly discovered installations within the synchronization scope are
  present in the Installation Catalog and classified as `New`.
- Installations whose synchronization signature has changed are
  classified as `Updated`.
- Installations within the synchronization scope that were not found
  are reported as `Not Found`.
- Installations outside the synchronization scope remain unaffected.
- `Not Found` installations are removed only when explicitly selected
  for removal by the user.
- Installations that have not changed do not appear in the
  synchronization results.

## Business Rules

### BR-01 — Synchronization Scope

Only installations within the selected synchronization scope may be
discovered, updated, or evaluated as `Not Found`.

### BR-02 — Optional Installation Name Pattern

The installation name pattern is optional.

If no pattern is specified, filesystem discovery is not restricted by
installation name.

### BR-03 — Installation Name Pattern

The installation name pattern is an advanced mechanism for controlling
the synchronization scope.

It may be used both to reduce the number of installations examined
during synchronization and to deliberately synchronize only a selected
group of installations.

### BR-04 — Scope Exclusion

Installations outside the selected synchronization scope must not be
interpreted as `Not Found`.

### BR-05 — Unselected Formats

Installations belonging to plugin formats that were not selected by the
user must not be evaluated as `Not Found` during that synchronization.

### BR-06 — Missing Does Not Imply Removal

An installation classified as `Not Found` must not be automatically
removed from the Installation Catalog.

Removal requires an explicit user decision.

### BR-07 — Synchronization Signature

The system maintains a synchronization signature for each cataloged
installation.

An installation is classified as `Updated` when its current
synchronization signature differs from the signature stored in the
catalog.

The specific algorithm used to calculate the synchronization signature
is outside the scope of this use case.

### BR-08 — New Installation

An installation discovered within the synchronization scope that is
not present in the Installation Catalog is classified as `New`.

### BR-09 — Unchanged Installation

An installation whose current synchronization signature matches the
signature stored in the catalog is considered unchanged.

Unchanged installations are not presented in the synchronization
results.

### BR-10 — Plugin Discovery Result

The `Plugin names` action displays plugin information discovered from
the installation during the current synchronization operation.

It does not retrieve plugin information from the persistent Plugin
Catalog.

## User Interface Considerations

- The plugin format selection should allow the user to select any
  combination of available formats.
- The format selection interface should provide convenient actions to
  select all or deselect all available formats.
- The installation name pattern should be presented as an advanced,
  optional field.
- The interface should indicate that users who are not familiar with
  installation filenames or directory names can leave the field blank.
- Synchronization results should focus on installations requiring the
  user's attention.
- `New`, `Updated`, and `Not Found` installations should be clearly
  distinguishable.
- Unchanged installations should not be displayed in the result list.
- Each discovered installation may provide a `Plugin names` action.
- The `Plugin names` action should open a separate dialog showing the
  plugins discovered in that installation.

## Related Functional Requirements

- TBD