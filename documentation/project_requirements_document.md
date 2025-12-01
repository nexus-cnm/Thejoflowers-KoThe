# Thejoflowers-KoThe – Project Requirements Document

## 1. Project Overview

**Thejoflowers-KoThe** is a ready-to-go starter kit that lets developers spin up a modern single-page web application in minutes. At its core, it combines a Laravel-powered PHP backend with a Vue.js frontend and Inertia.js to bridge the two. Out of the box you get user registration and login, a basic task-management module (with full Create, Read, Update, Delete capabilities), and a polished AdminLTE Bootstrap theme for a professional look and feel.

We’re building this kit to save time on boilerplate work and enforce best practices in one swoop. Success means a developer can clone the repository, follow a short setup guide, and immediately start customizing rather than wrestling with authentication, routing, asset builds, and layout configuration.

## 2. In-Scope vs. Out-of-Scope

### In-Scope (Version 1.0)
- **User Authentication**: Registration, login, logout via Laravel Sanctum.
- **Task Management (CRUD)**: Create, list, edit, delete tasks, backed by UUID primary keys.
- **Inertia.js SPA Bridge**: Client-side navigation with server-driven page rendering.
- **AdminLTE Theme**: Pre-built sidebar, navbar, and responsive layout.
- **Build Pipeline**: Vite for fast asset compilation and SCSS support.
- **Database**: MySQL (configurable via `.env`).
- **Code Quality Tools**: ESLint, Prettier, and basic PHPUnit tests.

### Out-of-Scope (Planned for Later)
- Role-based permissions beyond basic auth.
- File uploads or media management.
- Real-time functionality (WebSockets, Pusher).
- Docker or containerized development environment.
- CI/CD pipeline configuration.
- Third-party integrations (payments, email services).

## 3. User Flow

A new user arrives at the welcome page and can sign up with their email and password. After clicking “Register,” they land on a dashboard protected by Laravel Sanctum. The dashboard uses a shared BaseLayout component that includes a collapsible sidebar, a top navbar, and a footer. If they’re not logged in, any attempt to visit a protected route redirects them to the login page.

Once authenticated, the user clicks “Tasks” in the sidebar. Inertia intercepts the click, sends an XHR request to the Laravel route, and returns a rendered Vue component with a paginated list of tasks. They can click “New Task” to open a form, fill in the title and description, submit, and see the list refresh without a full page reload. Each task row has “Edit” and “Delete” actions that open modals or confirm dialogs in the same flow.

## 4. Core Features

- **Authentication Module**: Registration, login, logout, password reset hooks.
- **Task CRUD Module**: Task list view, creation form, edit form, delete confirmation.
- **UUID Identifiers**: Each user and task uses a UUID primary key for security and uniqueness.
- **Inertia.js Navigation**: Seamless SPA experience with partial DOM updates.
- **Shared Layout**: `BaseLayout.vue` with AdminLTE styling—sidebar, header, footer.
- **Flash Notifications**: Success/error messages passed via Inertia props.
- **Asset Pipeline**: Vite + SCSS, hot module replacement in development.
- **Code Standards**: ESLint and Prettier for JS, PSR-12 and DocBlocks for PHP.
- **Testing**: PHPUnit for backend tests; placeholder for future E2E tests.

## 5. Tech Stack & Tools

- **Backend**: Laravel 10 (PHP ≥ 8.1) with MVC pattern, Eloquent ORM.
- **Authentication**: Laravel Sanctum for token and session auth.
- **Frontend**: Vue 3 + Inertia.js, single-file components (.vue).
- **Build Tool**: Vite for fast asset bundling and dev server.
- **CSS Framework**: Bootstrap 5 with the AdminLTE theme.
- **Database**: MySQL (configurable), migrations for schema.
- **Testing**: PHPUnit (backend); plan to add Cypress/Playwright later.
- **Code Quality**: ESLint, Prettier, PHP CS Fixer (optional).
- **Package Managers**: Composer (PHP), NPM/Yarn (JS).

## 6. Non-Functional Requirements

- **Performance**: Sub-200 ms server response for Inertia page loads; bundle size < 200 KB gzipped.
- **Security**: CSRF tokens on all forms, input validation on client and server, HTTPS enforcement.
- **Reliability**: 99.9% uptime of core routes; automatic retry logic for non-critical asset loads.
- **Usability**: Fully responsive design; WCAG AA color contrast for text and UI elements.
- **Maintainability**: 80%+ code coverage for PHP tests; linting errors must block PRs.

## 7. Constraints & Assumptions

- **Environment**: Requires PHP 8.1+, Node 16+, NPM/Yarn, MySQL 5.7+ (or MariaDB equivalent).
- **Package Availability**: Inertia.js, AdminLTE, and Laravel Sanctum must remain compatible with core framework versions.
- **Developer Setup**: Assumes developer has Composer and npm skills; no Docker support in v1.
- **API Limits**: No external API calls in v1, so rate limits are not a concern.

## 8. Known Issues & Potential Pitfalls

- **Vite HMR**: On Windows machines, hot reload can sometimes fail—clear cache or restart server.
- **UUID Collisions**: Extremely unlikely, but be cautious when manually seeding IDs.
- **Route Caching**: After adding or changing routes, developer must run `php artisan route:cache` or clear cache.
- **AdminLTE Upgrades**: Future AdminLTE major releases may introduce breaking CSS or JS changes.
- **E2E Testing Gap**: No end-to-end tests currently, so manual testing is required for UI flows.


---
*This document serves as the definitive reference for all subsequent technical documents.  Every feature, flow, and requirement outlined here is intended to leave no ambiguity for an AI or human engineer preparing architecture, file structures, and coding guidelines.*