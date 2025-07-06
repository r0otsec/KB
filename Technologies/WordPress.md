---
tags:
  - web
  - technologies
date: 2023-09-1
---
- Open-source `Content Management System (CMS)`.
- Written in PHP
- Backed by MySQL or MariaDB database.
# Components

- Core PHP-based app handles routing, templating, content, and plugin/theme APIs:
	- `index.php`, `wp-config.php`, `wp-load.php` (core files).
	- `wp-admin/` - admin dashboard backend
	- `wp-includes/` - libraries and core functions
	- `wp-content/` - user content, plugins, themes, uploads
- Database uses MySQL/MariaDB to store all dynamic content:
	- posts, pages, media metadata
	- users, roles, permissions
	- plugin/theme settings
- Themes
	- stored under `wp-content/themes`
# How It Works

- Typical workflow includes:
	- user visiting the site (`index.php`)
	- WP loads and routes the request.
	- system loads theme, db settings and plugins
	- WP queries the database to fetch content (via `wpdb`).
	- response rendered using theme templates.

