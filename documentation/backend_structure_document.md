# Backend Structure Document for Thejoflowers-KoThe

This document describes the backend setup for the Thejoflowers-KoThe starter kit. It explains the architecture, data management, APIs, hosting, infrastructure, security, and monitoring in plain language so that anyone can understand how the backend works.

## 1. Backend Architecture

### Overall Design
- The backend follows the **Model-View-Controller (MVC)** pattern provided by Laravel (PHP).  
- **Inertia.js** acts as a bridge between Laravel’s server-side routing and Vue.js’s client-side rendering, giving a seamless Single Page Application (SPA) feel without building a separate API for every view.
- **Vite** is used for fast asset bundling and hot module replacement during development.

### Scalability, Maintainability, Performance
- **Scalability**: Laravel can be scaled horizontally by adding more application servers behind a load balancer. Database scaling (read replicas) is possible with MySQL.
- **Maintainability**: Clear division into controllers, models, and views, plus shared layout components in Vue, keeps code organized and easy to update.
- **Performance**: Vite optimizes and splits assets automatically. Inertia only updates changed parts of the page, reducing full-page reloads.

## 2. Database Management

### Technology
- Type: **Relational (SQL)**
- System: **MySQL** (configurable through `.env`, can use MariaDB)

### Data Structure & Access
- **Eloquent ORM** maps database tables to PHP model classes for intuitive data handling.
- Migrations track and apply schema changes, ensuring every environment has the same database structure.
- Relationships (e.g., a User has many Tasks) are defined in models, making data retrieval straightforward.
- **UUIDs** are used as primary keys for `users` and `tasks` to ensure global uniqueness and security.

### Data Management Practices
- Use Laravel Form Requests for validating request data before it reaches controllers.  
- Seeders and factories help populate test data quickly.  
- Database transactions ensure data integrity when multiple tables are updated together.

## 3. Database Schema

### Human-Readable Overview

1. **users**  
   - Unique ID (UUID)  
   - Name, Email, Password  
   - Timestamps (created, updated)  

2. **tasks**  
   - Unique ID (UUID)  
   - Title, Description  
   - Status or completion flag  
   - Due date (optional)  
   - Belongs to a User (user_id as UUID)  
   - Timestamps (created, updated)  

3. **etapas** (stages or steps)  
   - ID (Auto-increment)  
   - Name, Description  
   - Timestamps (created, updated)

### SQL Schema (MySQL)
```sql
-- Users table
CREATE TABLE users (
  id CHAR(36) PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  email_verified_at DATETIME NULL,
  password VARCHAR(255) NOT NULL,
  remember_token VARCHAR(100) NULL,
  created_at TIMESTAMP NULL,
  updated_at TIMESTAMP NULL
);

-- Tasks table
CREATE TABLE tasks (
  id CHAR(36) PRIMARY KEY,
  user_id CHAR(36) NOT NULL,
  title VARCHAR(255) NOT NULL,
  description TEXT NULL,
  status ENUM('pending','completed') DEFAULT 'pending',
  due_date DATE NULL,
  created_at TIMESTAMP NULL,
  updated_at TIMESTAMP NULL,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- Etapas table
CREATE TABLE etapas (
  id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  description TEXT NULL,
  created_at TIMESTAMP NULL,
  updated_at TIMESTAMP NULL
);
```  

## 4. API Design and Endpoints

### Approach
- **Inertia.js**–powered routes in `routes/web.php` handle both page loading and data passing.  
- **RESTful** endpoints in `routes/api.php` (protected by Sanctum) expose JSON for any future mobile or external clients.

### Key Endpoints

**Authentication** (via Laravel Sanctum)  
- `GET /login` – show login page  
- `POST /login` – authenticate user, issue session  
- `POST /logout` – end session  
- `GET /register` – show registration page  
- `POST /register` – create new user  

**Tasks**  
- `GET /tasks` – list tasks (page, filter)  
- `GET /tasks/create` – show task-creation form  
- `POST /tasks` – save new task  
- `GET /tasks/{id}/edit` – show edit form  
- `PUT /tasks/{id}` – update task  
- `DELETE /tasks/{id}` – delete task  

**Etapas** (optional CRUD)  
- Similar endpoints under `/etapas` for creating, reading, updating, deleting steps or stages.

### Frontend-Backend Communication
- Inertia intercepts link clicks and form submissions, sends AJAX requests, and hydrates Vue components with JSON data from Laravel.

## 5. Hosting Solutions

### Environment
- **Cloud**: AWS (recommended)  
  - **EC2** instances run the Laravel application.  
  - **RDS (MySQL)** holds the database.  
  - **S3** for file storage (user‐uploaded files, backups).  
- **Alternative**: DigitalOcean Droplets + Managed Databases or Heroku with ClearDB.

### Benefits
- **Reliability**: Managed services (RDS, S3) offer high availability and automated backups.  
- **Scalability**: You can scale EC2 instances or add read replicas to RDS quickly.  
- **Cost-effectiveness**: Pay-as-you-go pricing lets you adjust resources as usage grows.

## 6. Infrastructure Components

- **Load Balancer** (AWS ELB) to distribute traffic across multiple app servers.  
- **Caching**: Laravel’s cache layer (file or Redis if enabled) speeds up repeated queries.  
- **Queue Worker**: Laravel Queue (Redis or database driver) for background jobs (emails, reports).  
- **CDN**: AWS CloudFront or similar for serving static assets (JS, CSS, images) globally with low latency.

## 7. Security Measures

- **Authentication & Authorization**: Laravel Sanctum for SPA tokens, middleware (`Authenticate`) protects routes.  
- **CSRF Protection**: Built-in Laravel CSRF tokens guard form submissions.  
- **Data Encryption**: Passwords hashed using bcrypt. HTTPS enforced on all endpoints.  
- **Input Validation**: Server-side validation via Form Requests prevents invalid or malicious data.  
- **Environment Isolation**: `.env` file stores secrets, not committed to source control.

## 8. Monitoring and Maintenance

- **Logging**: Laravel’s Monolog integration writes logs to storage and can forward to CloudWatch or an ELK stack.  
- **Error Tracking**: Tools like Sentry or Bugsnag can be integrated for real-time exception alerts.  
- **Performance Monitoring**: New Relic or Laravel Telescope for query/route timing insights.  
- **CI/CD**: GitHub Actions or GitLab CI can run PHPUnit and ESLint/Prettier checks on each pull request.  
- **Backups & Migrations**: Regular database backups and Laravel migrations ensure safe schema updates.

## 9. Conclusion and Overall Backend Summary

The Thejoflowers-KoThe backend is built on a proven Laravel MVC foundation, enhanced by Inertia.js and Vue.js for a modern SPA experience. It uses MySQL with UUIDs for secure, global primary keys and follows best practices in routing, data validation, and code organization. Hosted in a cloud environment (e.g., AWS), with load balancing, caching, and CDN support, it delivers reliable, scalable performance. Security is enforced at multiple layers—authentication, encryption, validation—and monitoring tools keep administrators informed. Overall, this structure provides a solid, maintainable, and high‐performance platform for rapid web application development.