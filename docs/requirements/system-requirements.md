# JAPMan — System Requirements Document
## 1. Objective
JAPMan (Java Audio Plugin Manager) aims to assist users in identifying, organizing, and searching for audio plugin installations available on their computer, as well as providing statistical information to support decision-making regarding future plugin acquisitions.
The system shall allow the user to maintain a registry of known plugins and associate these plugins with their respective installations found in the system.
## 2. Scope
The system's main functions will be:
    - to scan for existing plugin installations on the computer;
    - to maintain a catalog of found installations;
    - to allow the user to maintain a plugin registry;
    - to allow the association between registered plugins and found installations;
    - to allow searching for available installations and plugins;
    - to present consolidated catalog information through a dashboard.
The system will initially be developed for use on computers with the Linux operating system.
## 3. Fundamental Concepts
### 3.1 Plugin
An audio plugin is a software product developed by a manufacturer or developer, whose existence is independent of whether it is installed on the user's computer.
A plugin may have zero, one, or several installations on the computer.
### 3.2 Installation
An installation represents a concrete occurrence of a plugin found in the computer's file system.
An installation may correspond to a file, folder, or other structure used by the plugin format.
An installation may be associated with one or more plugins, while a plugin may have one or more installations.
### 3.3 Association
An association relates an installation found on the computer to a plugin registered by the user.
It will be up to the user to establish the associations between the cataloged installations and the registered plugins.
## 4. Functional Requirements
### RF-001 — Search
The system shall allow the user to search for audio plugins that have cataloged installations on the computer.
The search shall allow filtering and sorting by different criteria, including at least:
    - plugin format (LV2, VST, VST3, CLAP, etc.);
    - installation origin (native or from another operating system via bridge);
    - name or part of the name;
    - manufacturer;
    - installation or update date;
    - category;
    - emulation;
    - version;
    - tags;
    - instrument type, when applicable, such as piano, guitar, or synthesizer.
### RF-002 — Installation Scan
The system shall offer a scanning mechanism capable of locating plugin installations on the computer.
The user shall be able to configure the locations that will be used as starting points for the scan.
The scan shall identify and collect available information about the installations found.
At the end of the scan, the system shall report, when applicable:
    - new installations found;
    - previously cataloged installations that were not found in the scan;
    - changes detected in already cataloged installations.
The system shall present the scan results to the user before making changes to the catalog, according to the rules defined for the update process.
### RF-003 — Maintenance of the plugin registry
The system shall offer the user resources to maintain a plugin registry.
The user shall be able to register a plugin that does not yet exist in the catalog and maintain the information associated with it.
The information registered by the user shall be preserved during new scans of the installations.
### RF-004 — Association between plugins and installations
The system shall allow the user to associate cataloged installations with registered plugins.
The system shall allow the user to associate an installation with more than one plugin when the nature of the installation so requires.
The system shall allow a plugin to have multiple installations.
The system shall allow the user to change or remove existing associations.
Installations found during a scan that are not yet associated with a plugin shall remain identifiable as unassociated installations.
### RF-005 — Dashboard
The system shall present a dashboard as the initial screen, containing consolidated information about the catalog.
The dashboard shall present, at a minimum:
    - number of installations associated with plugins;
    - number of installations not yet associated;
    - distribution of installations by origin;
    - distribution of installations by manufacturer;
    - distribution of installations by format;
    - distribution of installations by category.
## 5. Non-Functional Requirements
### RNF-001 — Local Persistence
The system shall use an embedded database to store its information.
The system's operation shall not depend on an external database server.
### RNF-002 — Interface
The system shall offer a modern, clear, and interactive graphical interface, suitable for viewing, searching, and managing catalog information.
The interface shall use appropriate interaction and visual presentation resources whenever they contribute to the understanding and use of the system.
### RNF-003 — Dependencies
The system shall prioritize the use of established and appropriate libraries for obtaining plugin and installation metadata.
### RNF-004 — Performance
Search operations on the local catalog shall have a response time suitable for interactive use of the system.
Scan operations shall be performed in a way that minimizes their impact on normal computer use.
### RNF-005 — Extensibility
The system architecture shall allow the inclusion of new installation discovery mechanisms, plugin formats, and supported platforms without requiring extensive changes to the system core.
## 6. Restrictions
### RT-001 — Initial Platform
The first version of the system will be for the Linux operating system.
### RT-002 — Desktop Application
The system will be developed as a desktop application.
## 7. Open Questions
The questions below do not yet constitute requirements or definitive decisions and should be analyzed during development:
    - Should the result of a scan be applied automatically or will it depend on explicit user confirmation?
    - How should the identity of an already cataloged installation be determined?
    - In which situations might the system automatically suggest an association between an installation and a plugin?
    - How can the user review and correct automatically suggested associations?
    - How can distinct plugins be optionally grouped by the user for organizational and search purposes?
    - What criteria should be used to determine that an installation no longer exists?
    • What information should be maintained for each plugin format?
    • What performance metrics should be adopted when the expected catalog volume is better defined?
