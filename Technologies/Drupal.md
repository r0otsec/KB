---
tags:
  - technologies
  - web
date: 2023-09-1
---
- Open-source `Content Management System`.
- Builds and manages websites and web apps.
- Written in PHP.
- Modular:
	- can add/remove features via modules.
# Structure

- Standard folder structure:
	- `/sites/` - site specific configs, files
	- `/modules/` - contributed/custom modules
	- `/themes/` - UI/UX themes
	- `/core/` - Drupal core files
	- `/profiles` - installation profiles
	- `/composer.json` - PHP dependency manager
# Stack

- Typically deployed on a `LAMP` stack:
	- Linux
	- Apache (for NGINX)
	- MySQL / MariaDB / PostgreSQL
	- PHP
# Major Components

- `Node`: piece of content (page, article, blog post).
- `Module`: add new features (e.g. contact form).
- `Block`: reusable UI components placed into regions.
- `Taxonomy`: content classification system (tags, categories).
- `View`: query builder to display content dynamically
- `Entity`: base content object (nodes, users, comments, etc.)
- `Theme`: define site appearance.
- `User Role`: permission sets

