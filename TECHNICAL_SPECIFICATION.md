# Technical Specification: Thejoflowers Web Application
*Company Profile + Marketplace/E-Commerce Korean Florist Platform*

## Table of Contents

1. [Project Overview](#project-overview)
2. [Technical Architecture](#technical-architecture)
3. [UI/UX Design System](#uiux-design-system)
4. [Feature Specifications](#feature-specifications)
5. [Database Design](#database-design)
6. [API Endpoints](#api-endpoints)
7. [Security & Authentication](#security--authentication)
8. [Payment & Shipping Integration](#payment--shipping-integration)
9. [Internationalization](#internationalization)
10. [Deployment & Infrastructure](#deployment--infrastructure)
11. [Development Workflow](#development-workflow)
12. [Testing Strategy](#testing-strategy)
13. [Performance Optimization](#performance-optimization)
14. [Maintenance & Support](#maintenance--support)

---

## Project Overview

### Project Name
**Thejoflowers** - Korean-style florist marketplace platform

### Project Type
Company Profile + E-Commerce / Marketplace platform

### Target Audience
- Individual customers looking for Korean-style floral arrangements
- Corporate clients for events and gifting
- Flower enthusiasts interested in Korean floral aesthetics

### Business Model
B2C e-commerce with single-location marketplace model

---

## Technical Architecture

### Technology Stack

#### Backend
- **Framework**: Laravel 11
- **Authentication**: Laravel Jetstream (Inertia + Vue + Sessions)
- **Database**: MySQL 8.0+
- **ORM**: Eloquent ORM
- **File Storage**: Laravel Filesystem (local/S3)
- **Queue System**: Redis + Laravel Horizon
- **Cache**: Redis

#### Frontend
- **Framework**: Vue 3 (Composition API)
- **Routing**: Inertia.js
- **UI Library**: Tailwind CSS 3.x
- **State Management**: Pinia
- **Build Tool**: Vite
- **Icons**: Heroicons
- **Forms**: Laravel Form + Vue components

#### Third-Party Integrations
- **Payment Gateway**: Midtrans Snap
- **Shipping**: RajaOngkir API
- **Email**: Mailgun/SendGrid
- **Image Processing**: Image Intervention
- **PDF Generation**: DomPDF

### System Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │    Backend      │    │  External APIs  │
│   (Vue 3)       │    │  (Laravel 11)   │    │                 │
│                 │    │                 │    │                 │
│ • UI Components │◄──►│ • Controllers   │◄──►│ • Midtrans      │
│ • State Mgmt    │    │ • Middleware    │    │ • RajaOngkir    │
│ • Routing       │    │ • Validation    │    │ • Storage (S3)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │
                              ▼
                       ┌─────────────────┐
                       │   Database      │
                       │   (MySQL)       │
                       │                 │
                       │ • Products      │
                       │ • Users         │
                       │ • Orders        │
                       │ • Categories    │
                       └─────────────────┘
```

---

## UI/UX Design System

### Theme: "Sky Bloom Garden" Korean Florist

### Color Palette
```css
/* Primary Colors */
--sky-blue-primary: #4496CA;
--cloud-blue-secondary: #D7ECFA;
--sunshine-yellow-cta: #F7D74C;
--pastel-meadow-green: #B7D8A8;
--warm-beige-cream: #F3E8D3;
--coral-peach-highlight: #F6B6A5;
--soft-brown-text: #A97C50;

/* Semantic Colors */
--success: #10B981;
--warning: #F59E0B;
--error: #EF4444;
--info: #3B82F6;
```

### Typography
```css
/* Font Family */
--font-primary: 'Inter', sans-serif;
--font-accent: 'Playfair Display', serif;

/* Font Scale */
--text-xs: 0.75rem;    /* 12px */
--text-sm: 0.875rem;   /* 14px */
--text-base: 1rem;     /* 16px */
--text-lg: 1.125rem;   /* 18px */
--text-xl: 1.25rem;    /* 20px */
--text-2xl: 1.5rem;    /* 24px */
--text-3xl: 1.875rem;  /* 30px */
--text-4xl: 2.25rem;   /* 36px */
```

### Design Tokens
```css
/* Spacing */
--space-1: 0.25rem;
--space-2: 0.5rem;
--space-3: 0.75rem;
--space-4: 1rem;
--space-5: 1.25rem;
--space-6: 1.5rem;
--space-8: 2rem;
--space-10: 2.5rem;
--space-12: 3rem;
--space-16: 4rem;

/* Border Radius */
--radius-sm: 0.375rem;
--radius-md: 0.5rem;
--radius-lg: 0.75rem;
--radius-xl: 1rem;
--radius-2xl: 1.5rem;

/* Shadows */
--shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
--shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1);
--shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1);
--shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1);
```

### Component Guidelines

#### Buttons
- **Primary CTA**: Sunshine Yellow background, dark text
- **Secondary**: Sky Blue background, white text
- **Outline**: Sky Blue border, white background
- **Size**: Large (48px height) for main actions

#### Cards
- **Background**: Warm Beige or White
- **Border Radius**: 1rem to 1.5rem
- **Padding**: 1.5rem
- **Shadow**: Soft dreamy shadows

#### Forms
- **Input**: White background, rounded-lg
- **Labels**: Soft brown color, font-semibold
- **Validation**: Coral peach for errors

---

## Feature Specifications

### 1. Company Profile Features

#### 1.1 Home Page
**Route**: `/`

**Components**:
- Hero banner with carousel (promotional content)
- Featured categories display
- Best-selling products carousel
- Current promotions banner
- Instagram feed integration (optional)
- Customer testimonials

**Technical Requirements**:
- Responsive design (mobile-first)
- Lazy loading for images
- SEO optimization
- Meta tags management

#### 1.2 About Page
**Route**: `/about`

**Content Sections**:
- Company story
- Our team
- Korean floral philosophy
- Store location and hours
- Certifications and awards

#### 1.3 Contact Page
**Route**: `/contact`

**Features**:
- Contact form with validation
- Interactive map (Google Maps)
- Business hours display
- Contact information cards
- Social media links

#### 1.4 Gallery Page
**Route**: `/gallery`

**Features**:
- Photo gallery with filtering
- Masonry layout
- Lightbox functionality
- Category filters (weddings, events, etc.)

### 2. E-Commerce Features

#### 2.1 Product Catalog
**Route**: `/products`

**Features**:
- Grid/List view toggle
- Search functionality
- Category filtering
- Price range slider
- Sort options (price, popularity, newness)
- Pagination with infinite scroll option
- Quick view functionality

**Technical Requirements**:
- Elasticsearch/MySQL full-text search
- Redis caching for popular products
- Image optimization (WebP format)

#### 2.2 Product Detail Page
**Route**: `/products/{slug}`

**Features**:
- Product image gallery with zoom
- Product information display
- Size/variation selection
- Add to cart functionality
- Related products recommendations
- Customer reviews and ratings
- Stock availability indicator
- Estimated delivery time

#### 2.3 Shopping Cart
**Route**: `/cart`

**Features**:
- Cart items management (add, remove, update)
- Quantity adjustment
- Coupon code application
- Subtotal calculation
- Proceed to checkout button
- Saved items for later

#### 2.4 Checkout Process
**Route**: `/checkout`

**Multi-step Process**:
1. **Shipping Information**
   - Address form with validation
   - Address book for logged-in users
   - Guest checkout option

2. **Shipping Method**
   - RajaOngkir integration
   - Real-time cost calculation
   - Delivery time estimates

3. **Payment Method**
   - Midtrans Snap integration
   - Multiple payment options
   - Voucher application

4. **Order Review**
   - Final order summary
   - Terms and conditions
   - Place order button

#### 2.5 Order Management
**Routes**: `/orders`, `/orders/{id}`

**Features**:
- Order history listing
- Order detail view
- Status tracking
- Invoice download
- Reorder functionality

### 3. User Management System

#### 3.1 Authentication
**Routes**: `/login`, `/register`, `/forgot-password`

**Features**:
- Social login options (Google, Facebook)
- Email verification
- Password reset functionality
- Remember me option
- Session management

#### 3.2 User Profile
**Route**: `/profile`

**Sections**:
- Personal information
- Address book
- Order history
- Wishlist
- Account settings
- Payment methods (saved)

### 4. Admin Dashboard

#### 4.1 Dashboard Overview
**Route**: `/admin`

**Metrics**:
- Today's revenue
- Order statistics
- Product performance
- Customer count
- Low stock alerts

#### 4.2 Product Management
**Routes**: `/admin/products`, `/admin/products/create`, `/admin/products/{id}/edit`

**Features**:
- CRUD operations for products
- Bulk actions
- Product variants management
- Image gallery management
- Inventory tracking
- SEO metadata management

#### 4.3 Category Management
**Routes**: `/admin/categories`

**Features**:
- Hierarchical categories
- Category images
- Sort order management
- SEO settings

#### 4.4 Order Management
**Routes**: `/admin/orders`

**Features**:
- Order listing with filters
- Status management
- Order detail view
- Invoice generation
- Shipping label generation
- Refund processing

#### 4.5 Finance Module
**Routes**: `/admin/finance`

**Features**:
- Income tracking (Midtrans webhook)
- Expense management
- Sales reports by product
- Revenue analytics
- Cash flow statements
- PDF/Excel export functionality
- Visual charts and graphs

#### 4.6 Other Management Modules
- **Banner Management**: Homepage banners, promotional banners
- **Gallery Management**: Photo gallery content
- **Voucher Management**: Discount codes, promotional codes
- **User Management**: Customer accounts, admin roles
- **Settings**: Store configuration, payment settings

### 5. Language Switcher (ID/EN)

#### 5.1 Implementation
- Laravel's built-in localization system
- Inertia shared props for translations
- Language preference storage (session/cookie)
- Dynamic language switching without page reload

#### 5.2 Features
- Language toggle in navigation bar
- Flag icons for language identification
- Persistent language selection
- URL-based language routing (optional)
- Admin panel for translation management

---

## Database Design

### Entity Relationship Diagram

```mermaid
erDiagram
    USERS {
        bigint id PK
        string name
        string email
        string password
        enum role
        timestamp email_verified_at
        string phone
        text address
        string city
        string province
        string postal_code
        timestamps
    }

    CATEGORIES {
        bigint id PK
        string name
        string slug
        text description
        string image
        bigint parent_id FK
        integer sort_order
        boolean is_active
        timestamps
    }

    PRODUCTS {
        bigint id PK
        string name
        string slug
        text description
        longtext content
        decimal price
        decimal compare_price
        integer stock_quantity
        string sku
        decimal weight
        integer category_id FK
        boolean is_active
        boolean is_featured
        timestamps
    }

    PRODUCT_IMAGES {
        bigint id PK
        bigint product_id FK
        string image_path
        string alt_text
        integer sort_order
        timestamps
    }

    PRODUCT_VARIANTS {
        bigint id PK
        bigint product_id FK
        string name
        string sku
        decimal price
        integer stock_quantity
        boolean is_active
        timestamps
    }

    CARTS {
        bigint id PK
        bigint user_id FK
        string session_id
        timestamps
    }

    CART_ITEMS {
        bigint id PK
        bigint cart_id FK
        bigint product_id FK
        bigint variant_id FK
        integer quantity
        decimal price
        timestamps
    }

    ORDERS {
        bigint id PK
        string order_number
        bigint user_id FK
        string status
        decimal subtotal
        decimal shipping_cost
        decimal tax
        decimal total
        string payment_status
        string payment_method
        json payment_details
        json shipping_address
        json billing_address
        timestamps
    }

    ORDER_ITEMS {
        bigint id PK
        bigint order_id FK
        bigint product_id FK
        bigint variant_id FK
        string product_name
        integer quantity
        decimal unit_price
        decimal total_price
        timestamps
    }

    VOUCHERS {
        bigint id PK
        string code
        string name
        text description
        enum type
        decimal value
        decimal minimum_amount
        integer usage_limit
        integer used_count
        timestamp starts_at
        timestamp expires_at
        boolean is_active
        timestamps
    }

    BANNERS {
        bigint id PK
        string title
        text description
        string image
        string link
        string position
        integer sort_order
        boolean is_active
        timestamps
    }

    GALLERY_IMAGES {
        bigint id PK
        string title
        text description
        string image
        string category
        integer sort_order
        boolean is_active
        timestamps
    }

    TRANSACTIONS {
        bigint id PK
        bigint order_id FK
        string type
        decimal amount
        text description
        json metadata
        timestamps
    }

    SHIPPING_RATES {
        bigint id PK
        string city
        string province
        string courier
        string service
        decimal cost
        integer etd_min
        integer etd_max
        timestamps
    }

    %% Relationships
    USERS ||--o{ ORDERS : places
    USERS ||--o{ CARTS : owns
    CATEGORIES ||--o{ PRODUCTS : contains
    CATEGORIES ||--o{ CATEGORIES : parent_of
    PRODUCTS ||--o{ PRODUCT_IMAGES : has
    PRODUCTS ||--o{ PRODUCT_VARIANTS : has
    PRODUCTS ||--o{ CART_ITEMS : in
    PRODUCTS ||--o{ ORDER_ITEMS : in
    CARTS ||--o{ CART_ITEMS : contains
    ORDERS ||--o{ ORDER_ITEMS : contains
    ORDERS ||--o{ TRANSACTIONS : has
```

### Migration Details

#### Core Tables

**users**
```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('customer', 'admin') DEFAULT 'customer',
    phone VARCHAR(20),
    address TEXT,
    city VARCHAR(100),
    province VARCHAR(100),
    postal_code VARCHAR(10),
    email_verified_at TIMESTAMP NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

**products**
```sql
CREATE TABLE products (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    description TEXT,
    content LONGTEXT,
    price DECIMAL(10,2) NOT NULL,
    compare_price DECIMAL(10,2),
    stock_quantity INT DEFAULT 0,
    sku VARCHAR(100) UNIQUE,
    weight DECIMAL(8,2) NOT NULL,
    category_id BIGINT,
    is_active BOOLEAN DEFAULT TRUE,
    is_featured BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

**orders**
```sql
CREATE TABLE orders (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    order_number VARCHAR(50) UNIQUE NOT NULL,
    user_id BIGINT,
    status ENUM('pending', 'confirmed', 'processing', 'shipped', 'delivered', 'cancelled') DEFAULT 'pending',
    payment_status ENUM('pending', 'paid', 'failed', 'refunded') DEFAULT 'pending',
    payment_method VARCHAR(50),
    payment_details JSON,
    subtotal DECIMAL(10,2) NOT NULL,
    shipping_cost DECIMAL(10,2) DEFAULT 0,
    tax DECIMAL(10,2) DEFAULT 0,
    total DECIMAL(10,2) NOT NULL,
    shipping_address JSON,
    billing_address JSON,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

---

## API Endpoints

### Authentication Endpoints

```
POST /api/register          - User registration
POST /api/login             - User login
POST /api/logout            - User logout
POST /api/forgot-password   - Request password reset
POST /api/reset-password    - Reset password
GET  /api/user              - Get current user
PUT  /api/user              - Update user profile
```

### Product Endpoints

```
GET  /api/products          - List products with filters
GET  /api/products/{slug}   - Get product details
GET  /api/products/search   - Search products
GET  /api/categories        - List categories
GET  /api/categories/{slug} - Get category with products
```

### Cart Endpoints

```
GET  /api/cart              - Get cart contents
POST /api/cart/add          - Add item to cart
PUT  /api/cart/update       - Update cart item
DELETE /api/cart/remove     - Remove item from cart
POST /api/cart/clear        - Clear cart
```

### Order Endpoints

```
GET  /api/orders            - Get user orders
GET  /api/orders/{id}       - Get order details
POST /api/orders            - Create new order
PUT  /api/orders/{id}       - Update order
GET  /api/orders/{id}/track - Track order status
```

### Payment Endpoints

```
POST /api/payment/midtrans  - Create Midtrans payment
POST /api/payment/callback   - Midtrans callback handler
POST /api/payment/status     - Check payment status
```

### Shipping Endpoints

```
GET  /api/shipping/cities   - Get cities list
GET  /api/shipping/cost     - Calculate shipping cost
POST /api/shipping/webhook  - RajaOngkir webhook
```

### Admin Endpoints

```
# Protected with admin middleware
GET  /api/admin/dashboard   - Dashboard statistics
GET  /api/admin/products    - Admin product list
POST /api/admin/products    - Create product
PUT  /api/admin/products/{id} - Update product
DELETE /api/admin/products/{id} - Delete product

GET  /api/admin/orders      - Admin order list
PUT  /api/admin/orders/{id} - Update order status

GET  /api/admin/finance     - Financial data
POST /api/admin/finance/expense - Add expense
GET  /api/admin/finance/reports - Financial reports
```

---

## Security & Authentication

### Authentication System
- **Laravel Jetstream**: Complete auth scaffolding
- **Session-based authentication**: For web users
- **API Tokens**: For admin operations
- **Two-factor authentication**: Optional security enhancement

### Security Measures

#### Input Validation
```php
// Product validation example
'product' => [
    'name' => 'required|string|max:255',
    'price' => 'required|numeric|min:0',
    'description' => 'nullable|string|max:1000',
    'category_id' => 'required|exists:categories,id',
    'images.*' => 'image|mimes:jpeg,png,jpg|max:2048'
];
```

#### Rate Limiting
```php
// API rate limiting
Route::middleware('throttle:60,1')->group(function () {
    Route::apiResource('products', ProductController::class);
});
```

#### CORS Configuration
```php
// config/cors.php
'paths' => ['api/*'],
'allowed_methods' => ['*'],
'allowed_origins' => [env('FRONTEND_URL')],
'allowed_headers' => ['*'],
```

#### CSRF Protection
- Enabled for all web routes
- CSRF token validation on forms
- XSRF-TOKEN cookie for JavaScript requests

#### File Upload Security
```php
// Secure file upload
'products' => [
    'image' => 'required|file|image|mimes:jpeg,png|max:2048',
    'dimensions:min_width=300,min_height=300'
];
```

#### Payment Security
- Midtrans signature verification
- Order amount validation
- Webhook signature validation
- Payment retry limits

---

## Payment & Shipping Integration

### Payment Gateway: Midtrans Snap

#### Configuration
```php
// config/midtrans.php
return [
    'server_key' => env('MIDTRANS_SERVER_KEY'),
    'client_key' => env('MIDTRANS_CLIENT_KEY'),
    'is_production' => env('MIDTRANS_IS_PRODUCTION', false),
    'is_sanitized' => true,
    'is_3ds' => true,
];
```

#### Implementation Flow
1. **Customer Checkout**: Collect shipping details
2. **Create Order**: Generate order in database
3. **Midtrans Request**: Create Snap token
4. **Payment Modal**: Display Midtrans payment interface
5. **Webhook**: Process payment notification
6. **Order Update**: Update order status

#### Supported Payment Methods
- Credit/Debit Cards (Visa, MasterCard, JCB)
- E-Wallets (GoPay, OVO, Dana, ShopeePay)
- Virtual Accounts (BCA, BNI, BRI, Mandiri)
- Convenience Stores (Alfamart, Indomaret)
- QRIS payments

### Shipping Integration: RajaOngkir

#### Configuration
```php
// config/rajaongkir.php
return [
    'api_key' => env('RAJAONGKIR_API_KEY'),
    'account_type' => env('RAJAONGKIR_ACCOUNT_TYPE', 'starter'), // starter, basic, pro
    'courier' => ['jne', 'tiki', 'pos'],
    'origin' => env('STORE_CITY_ID'), // Store location city ID
];
```

#### Features
- **Real-time shipping cost calculation**
- **Multiple courier options**
- **Delivery time estimation**
- **Tracking information**

#### Implementation Flow
1. **Shipping Form**: Collect destination address
2. **Cost Calculation**: Query RajaOngkir API
3. **Display Options**: Show available couriers and costs
4. **User Selection**: Customer chooses shipping method
5. **Save to Order**: Store shipping details with order

---

## Internationalization (ID/EN)

### Laravel Localization Setup

#### Language Files Structure
```
resources/
├── lang/
│   ├── en/
│   │   ├── common.php
│   │   ├── auth.php
│   │   ├── products.php
│   │   ├── checkout.php
│   │   └── validation.php
│   └── id/
│       ├── common.php
│       ├── auth.php
│       ├── products.php
│       ├── checkout.php
│       └── validation.php
```

#### Example Language File
```php
// resources/lang/en/common.php
return [
    'welcome' => 'Welcome',
    'products' => 'Products',
    'cart' => 'Cart',
    'checkout' => 'Checkout',
    'contact' => 'Contact',
    'about' => 'About',
    'search' => 'Search',
    'price' => 'Price',
    'quantity' => 'Quantity',
    'total' => 'Total',
];
```

```php
// resources/lang/id/common.php
return [
    'welcome' => 'Selamat Datang',
    'products' => 'Produk',
    'cart' => 'Keranjang',
    'checkout' => 'Checkout',
    'contact' => 'Kontak',
    'about' => 'Tentang',
    'search' => 'Cari',
    'price' => 'Harga',
    'quantity' => 'Jumlah',
    'total' => 'Total',
];
```

### Frontend Implementation

#### Language Switcher Component
```vue
<!-- Components/LanguageSwitcher.vue -->
<template>
    <div class="relative">
        <button @click="toggleDropdown"
                class="flex items-center space-x-2 px-3 py-2 rounded-lg hover:bg-white/10 transition-colors">
            <span class="text-2xl">{{ currentLocale.flag }}</span>
            <span class="font-medium">{{ currentLocale.name }}</span>
        </button>

        <div v-if="isOpen" class="absolute right-0 mt-2 w-48 bg-white rounded-lg shadow-lg py-2 z-50">
            <button v-for="locale in locales"
                    :key="locale.code"
                    @click="switchLanguage(locale.code)"
                    class="w-full flex items-center space-x-3 px-4 py-2 hover:bg-gray-100 transition-colors">
                <span class="text-xl">{{ locale.flag }}</span>
                <span class="text-gray-700">{{ locale.name }}</span>
            </button>
        </div>
    </div>
</template>
```

#### Middleware for Language Detection
```php
// app/Http/Middleware/SetLocale.php
class SetLocale
{
    public function handle($request, Closure $next)
    {
        if (session()->has('locale')) {
            app()->setLocale(session('locale'));
        } else {
            // Detect from browser or use default
            $locale = $request->getPreferredLanguage(['en', 'id']);
            app()->setLocale($locale);
            session(['locale' => $locale]);
        }

        return $next($request);
    }
}
```

#### Shared Translations with Inertia
```php
// app/Providers/AppServiceProvider.php
public function boot()
{
    Inertia::share([
        'translations' => function () {
            return [
                'common' => __('common'),
                'auth' => __('auth'),
                'products' => __('products'),
                'checkout' => __('checkout'),
            ];
        },
        'locale' => function () {
            return [
                'current' => app()->getLocale(),
                'available' => config('app.available_locales', ['en', 'id']),
            ];
        },
    ]);
}
```

#### Vue Translation Helper
```javascript
// resources/js/Translations.js
export default {
    methods: {
        __(key, parameters = {}) {
            const translation = this.$page.props.translations;
            const value = this.getNestedValue(translation, key);

            if (!value) {
                console.warn(`Translation missing: ${key}`);
                return key;
            }

            return this.replaceParameters(value, parameters);
        },

        getNestedValue(obj, path) {
            return path.split('.').reduce((current, key) => {
                return current && current[key] !== undefined ? current[key] : null;
            }, obj);
        },

        replaceParameters(str, params) {
            return str.replace(/:(\w+)/g, (match, key) => {
                return params[key] !== undefined ? params[key] : match;
            });
        }
    }
};
```

---

## Deployment & Infrastructure

### Production Environment

#### Server Requirements
- **Web Server**: Nginx 1.20+ or Apache 2.4+
- **PHP**: 8.2+ with required extensions
- **Database**: MySQL 8.0+ or MariaDB 10.6+
- **Cache**: Redis 6.0+
- **Queue**: Redis or Supervisor
- **SSL**: Let's Encrypt certificate

#### Directory Structure
```
/var/www/thejoflowers/
├── public/                    # Web root
├── storage/                   # File uploads, logs
├── bootstrap/cache/          # Framework cache
├── vendor/                   # Composer dependencies
├── node_modules/            # NPM dependencies
├── .env                     # Environment configuration
└── artisan                  # Laravel CLI tool
```

#### Nginx Configuration
```nginx
server {
    listen 80;
    server_name thejoflowers.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name thejoflowers.com;

    ssl_certificate /etc/letsencrypt/live/thejoflowers.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/thejoflowers.com/privkey.pem;

    root /var/www/thejoflowers/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

### Environment Configuration

#### .env.example
```env
APP_NAME="Thejoflowers"
APP_ENV=production
APP_KEY=base64:your-key-here
APP_DEBUG=false
APP_URL=https://thejoflowers.com

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=thejoflowers
DB_USERNAME=your-db-user
DB_PASSWORD=your-db-password

BROADCAST_DRIVER=log
CACHE_DRIVER=redis
FILESYSTEM_DISK=local
QUEUE_CONNECTION=redis
SESSION_DRIVER=database
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailgun.org
MAIL_PORT=587
MAIL_USERNAME=your-mailgun-username
MAIL_PASSWORD=your-mailgun-password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=info@thejoflowers.com
MAIL_FROM_NAME="${APP_NAME}"

# File Storage
FILESYSTEM_CLOUD=s3
AWS_ACCESS_KEY_ID=your-aws-key
AWS_SECRET_ACCESS_KEY=your-aws-secret
AWS_DEFAULT_REGION=ap-southeast-1
AWS_BUCKET=thejoflowers-storage
AWS_URL=https://thejoflowers-storage.s3.amazonaws.com

# Midtrans Payment Gateway
MIDTRANS_SERVER_KEY=your-midtrans-server-key
MIDTRANS_CLIENT_KEY=your-midtrans-client-key
MIDTRANS_IS_PRODUCTION=true

# RajaOngkir Shipping API
RAJAONGKIR_API_KEY=your-rajaongkir-api-key
RAJAONGKIR_ACCOUNT_TYPE=pro
STORE_CITY_ID=your-store-city-id
```

### Deployment Pipeline

#### Continuous Integration (GitHub Actions)
```yaml
# .github/workflows/deploy.yml
name: Deploy to Production

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        cache: 'npm'

    - name: Setup PHP
      uses: shivammathur/setup-php@v2
      with:
        php-version: '8.2'
        extensions: bcmath, ctype, fileinfo, json, mbstring, openssl, pdo, tokenizer, xml

    - name: Install Dependencies
      run: |
        composer install --no-dev --optimize-autoloader
        npm ci
        npm run build

    - name: Deploy to Server
      uses: appleboy/ssh-action@v0.1.5
      with:
        host: ${{ secrets.HOST }}
        username: ${{ secrets.USERNAME }}
        key: ${{ secrets.SSH_KEY }}
        script: |
          cd /var/www/thejoflowers
          git pull origin main
          composer install --no-dev --optimize-autoloader
          npm ci
          npm run build
          php artisan config:cache
          php artisan route:cache
          php artisan view:cache
          php artisan migrate --force
          supervisorctl restart laravel-worker
```

---

## Development Workflow

### Local Development Setup

#### Prerequisites
- **PHP 8.2+**: With required extensions
- **Composer**: Dependency manager
- **Node.js 18+**: Frontend build tools
- **MySQL 8.0+**: Database
- **Redis**: Cache and queue driver

#### Installation Steps

1. **Clone Repository**
```bash
git clone https://github.com/nexus-cnm/Thejoflowers-KoThe.git
cd Thejoflowers-KoThe
```

2. **Install Dependencies**
```bash
composer install
npm install
```

3. **Environment Setup**
```bash
cp .env.example .env
php artisan key:generate
```

4. **Database Setup**
```bash
php artisan migrate:fresh --seed
```

5. **Frontend Build**
```bash
npm run dev
```

6. **Start Development Server**
```bash
php artisan serve
```

### Code Standards

#### PHP Code Style
- **PSR-12**: Coding standard compliance
- **Laravel Pint**: Automatic code formatting
- **PHPStan**: Static analysis for code quality

#### JavaScript/Vue Code Style
- **ESLint**: Linting with recommended rules
- **Prettier**: Code formatting
- **TypeScript**: Type checking for better reliability

#### Configuration Files
```json
// .eslintrc.json
{
    "extends": [
        "plugin:vue/vue3-recommended",
        "eslint:recommended"
    ],
    "rules": {
        "vue/multi-word-component-names": "off",
        "vue/no-unused-vars": "error"
    }
}
```

```json
// .prettierrc
{
    "semi": true,
    "singleQuote": true,
    "tabWidth": 4,
    "trailingComma": "es5"
}
```

### Git Workflow

#### Branch Naming Convention
- `feature/feature-name`: New feature development
- `bugfix/bug-description`: Bug fixes
- `hotfix/urgent-fix`: Critical bug fixes
- `release/version-number`: Release preparation

#### Commit Message Format
```
type(scope): description

[optional body]

[optional footer]
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes
- `refactor`: Code refactoring
- `test`: Test additions
- `chore`: Maintenance tasks

**Examples**:
```
feat(checkout): implement Midtrans payment integration

Add support for credit card payments and e-wallet options
through Midtrans Snap service.

Closes #123
```

```
fix(products): resolve stock quantity sync issue

Fix bug where product stock wasn't updating correctly
after successful order completion.
```

---

## Testing Strategy

### Testing Pyramid

#### Unit Tests (70%)
- **Model Testing**: Validate model relationships and methods
- **Service Testing**: Test business logic in service classes
- **Helper Testing**: Validate utility functions
- **Component Testing**: Test individual Vue components

#### Feature/Integration Tests (20%)
- **API Endpoint Testing**: Validate request/response cycles
- **User Journey Testing**: Test complete user workflows
- **Database Integration**: Validate data persistence

#### End-to-End Tests (10%)
- **Critical Path Testing**: Test important user flows
- **Cross-browser Testing**: Ensure compatibility
- **Performance Testing**: Load and stress testing

### Testing Tools

#### PHP Testing
```bash
# Run all tests
php artisan test

# Run specific test file
php artisan test tests/Unit/ProductTest.php

# Generate code coverage
php artisan test --coverage
```

#### JavaScript Testing
```bash
# Run Jest tests
npm run test

# Run Cypress E2E tests
npm run test:e2e
```

### Example Test Cases

#### Unit Test Example
```php
// tests/Unit/ProductServiceTest.php
class ProductServiceTest extends TestCase
{
    use RefreshDatabase;

    public function test_can_create_product_with_variants()
    {
        $category = Category::factory()->create();
        $productData = Product::factory()->make([
            'category_id' => $category->id
        ])->toArray();

        $product = $this->productService->create($productData);

        $this->assertInstanceOf(Product::class, $product);
        $this->assertEquals($productData['name'], $product->name);
        $this->assertEquals($category->id, $product->category_id);
    }

    public function test_calculates_cart_total_correctly()
    {
        $cart = Cart::factory()->create();
        $items = CartItem::factory()->count(3)->create([
            'cart_id' => $cart->id
        ]);

        $total = $this->cartService->calculateTotal($cart);
        $expectedTotal = $items->sum(function ($item) {
            return $item->quantity * $item->price;
        });

        $this->assertEquals($expectedTotal, $total);
    }
}
```

#### Feature Test Example
```php
// tests/Feature/CheckoutTest.php
class CheckoutTest extends TestCase
{
    use RefreshDatabase;

    public function test_user_can_complete_checkout_flow()
    {
        $user = User::factory()->create();
        $product = Product::factory()->create(['price' => 100000]);

        $this->actingAs($user)
            ->post('/cart/add', [
                'product_id' => $product->id,
                'quantity' => 2
            ]);

        $this->actingAs($user)
            ->post('/checkout', [
                'shipping_address' => [
                    'name' => 'John Doe',
                    'phone' => '08123456789',
                    'address' => 'Jl. Test No. 123',
                    'city' => 'Jakarta',
                    'province' => 'DKI Jakarta',
                    'postal_code' => '12345'
                ],
                'shipping_method' => 'jne_reg',
                'payment_method' => 'midtrans'
            ])
            ->assertRedirect()
            ->assertSessionHas('success');

        $this->assertDatabaseHas('orders', [
            'user_id' => $user->id,
            'total' => 200000,
            'status' => 'pending'
        ]);
    }
}
```

#### Vue Component Test Example
```javascript
// tests/js/components/ProductCard.test.js
import { mount } from '@vue/test-utils'
import ProductCard from '@/Components/ProductCard.vue'

describe('ProductCard', () => {
    const mockProduct = {
        id: 1,
        name: 'Beautiful Rose Bouquet',
        price: 150000,
        image: '/images/product.jpg',
        slug: 'beautiful-rose-bouquet'
    }

    it('renders product information correctly', () => {
        const wrapper = mount(ProductCard, {
            props: { product: mockProduct }
        })

        expect(wrapper.text()).toContain(mockProduct.name)
        expect(wrapper.text()).toContain('Rp 150.000')
        expect(wrapper.find('img').attributes('src')).toBe(mockProduct.image)
    })

    it('emits add-to-cart event when button clicked', async () => {
        const wrapper = mount(ProductCard, {
            props: { product: mockProduct }
        })

        await wrapper.find('[data-testid="add-to-cart"]').trigger('click')

        expect(wrapper.emitted('add-to-cart')).toBeTruthy()
        expect(wrapper.emitted('add-to-cart')[0]).toEqual([mockProduct])
    })
})
```

---

## Performance Optimization

### Frontend Optimization

#### Asset Optimization
```javascript
// vite.config.js
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
    build: {
        rollupOptions: {
            output: {
                manualChunks: {
                    vendor: ['vue', '@inertiajs/vue3'],
                    ui: ['@headlessui/vue', 'heroicons'],
                }
            }
        },
        minify: 'terser',
        sourcemap: false,
    },
    css: {
        postcss: {
            plugins: [
                require('autoprefixer'),
                require('cssnano')({ preset: 'default' })
            ]
        }
    }
});
```

#### Image Optimization
```php
// App/Http/Controllers/ProductController.php
public function show($slug)
{
    $product = Product::with(['images', 'category'])
        ->where('slug', $slug)
        ->firstOrFail();

    // Optimize images for web
    $product->images->each(function ($image) {
        $image->url = Image::make($image->path)
            ->resize(800, 600, function ($constraint) {
                $constraint->aspectRatio();
                $constraint->upsize();
            })
            ->encode('webp', 80);
    });

    return Inertia::render('Products/Show', [
        'product' => $product
    ]);
}
```

#### Lazy Loading Implementation
```vue
<!-- Components/ProductList.vue -->
<template>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div v-for="(product, index) in products" :key="product.id">
            <ProductCard
                v-if="isVisible(index)"
                :product="product"
                :loading="false"
            />
            <div v-else class="animate-pulse bg-gray-200 h-64 rounded-lg"></div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            visibleItems: 6,
            loading: false
        }
    },
    methods: {
        loadMore() {
            this.visibleItems += 6;
        },
        isVisible(index) {
            return index < this.visibleItems;
        }
    }
}
</script>
```

### Backend Optimization

#### Database Optimization
```php
// App/Models/Product.php
class Product extends Model
{
    protected $with = ['category', 'images'];

    protected $casts = [
        'price' => 'decimal:2',
        'is_active' => 'boolean',
        'created_at' => 'datetime',
        'updated_at' => 'datetime'
    ];

    // Add indexes for frequently queried fields
    protected $indexes = [
        'name',
        'slug',
        'category_id',
        'is_active',
        'is_featured'
    ];
}
```

#### Caching Strategy
```php
// App/Http/Controllers/CategoryController.php
class CategoryController extends Controller
{
    public function index()
    {
        $categories = Cache::remember('categories.index', 3600, function () {
            return Category::with('children')
                ->where('is_active', true)
                ->whereNull('parent_id')
                ->orderBy('sort_order')
                ->get();
        });

        return response()->json($categories);
    }

    public function show($slug)
    {
        $cacheKey = "category.{$slug}";

        $category = Cache::remember($cacheKey, 1800, function () use ($slug) {
            return Category::with(['products.images', 'children'])
                ->where('slug', $slug)
                ->firstOrFail();
        });

        return Inertia::render('Categories/Show', [
            'category' => $category
        ]);
    }
}
```

#### Query Optimization
```php
// App/Http/Controllers/ProductController.php
class ProductController extends Controller
{
    public function search(Request $request)
    {
        $query = Product::with(['category', 'images'])
            ->where('is_active', true);

        // Apply filters efficiently
        if ($request->category) {
            $query->whereHas('category', function ($q) use ($request) {
                $q->where('slug', $request->category);
            });
        }

        if ($request->min_price) {
            $query->where('price', '>=', $request->min_price);
        }

        if ($request->max_price) {
            $query->where('price', '<=', $request->max_price);
        }

        // Use cursor for large datasets
        $products = $query->orderBy('created_at', 'desc')
            ->cursorPaginate(12);

        return response()->json($products);
    }
}
```

### Performance Monitoring

#### Laravel Telescope
```php
// config/telescope.php
'watchers' => [
    Watchers\CacheWatcher::class => true,
    Watchers\CommandWatcher::class => true,
    Watchers\DatabaseWatcher::class => true,
    Watchers\ModelWatcher::class => true,
    Watchers\RequestWatcher::class => true,
    Watchers\QueryWatcher::class => true,
    Watchers\RedisWatcher::class => true,
],
```

#### Frontend Performance Metrics
```javascript
// resources/js/mixins/performance.js
export default {
    mounted() {
        this.trackPageLoad();
    },

    methods: {
        trackPageLoad() {
            if (process.env.NODE_ENV === 'production') {
                const navigation = performance.getEntriesByType('navigation')[0];

                if (navigation) {
                    window.gtag('event', 'page_load_time', {
                        page: this.$page.url,
                        load_time: navigation.loadEventEnd - navigation.loadEventStart,
                        dom_content_loaded: navigation.domContentLoadedEventEnd - navigation.domContentLoadedEventStart
                    });
                }
            }
        }
    }
}
```

---

## Maintenance & Support

### Monitoring & Logging

#### Application Monitoring
- **Sentry**: Error tracking and performance monitoring
- **Uptime Robot**: Server uptime monitoring
- **Google Analytics**: User behavior analytics
- **Cloudflare**: CDN and security monitoring

#### Logging Configuration
```php
// config/logging.php
'channels' => [
    'daily' => [
        'driver' => 'daily',
        'path' => storage_path('logs/laravel.log'),
        'level' => env('LOG_LEVEL', 'debug'),
        'days' => 14,
    ],

    'errors' => [
        'driver' => 'daily',
        'path' => storage_path('logs/errors.log'),
        'level' => 'error',
        'days' => 30,
    ],

    'orders' => [
        'driver' => 'daily',
        'path' => storage_path('logs/orders.log'),
        'level' => 'info',
        'days' => 90,
    ],
],
```

### Backup Strategy

#### Database Backup
```bash
#!/bin/bash
# scripts/backup-database.sh

DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/var/backups/thejoflowers"
DB_NAME="thejoflowers"

# Create backup
mysqldump -u root -p$MYSQL_PASSWORD $DB_NAME > $BACKUP_DIR/db_backup_$DATE.sql

# Compress backup
gzip $BACKUP_DIR/db_backup_$DATE.sql

# Keep only last 30 days
find $BACKUP_DIR -name "db_backup_*.sql.gz" -mtime +30 -delete
```

#### File Backup
```bash
#!/bin/bash
# scripts/backup-files.sh

DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/var/backups/thejoflowers"
SOURCE_DIR="/var/www/thejoflowers/storage/app/public"

# Create tar archive
tar -czf $BACKUP_DIR/files_backup_$DATE.tar.gz -C $SOURCE_DIR .

# Keep only last 30 days
find $BACKUP_DIR -name "files_backup_*.tar.gz" -mtime +30 -delete
```

### Health Checks

#### Application Health Endpoint
```php
// routes/api.php
Route::get('/health', function () {
    return response()->json([
        'status' => 'ok',
        'timestamp' => now()->toISOString(),
        'services' => [
            'database' => $this->checkDatabase(),
            'cache' => $this->checkCache(),
            'storage' => $this->checkStorage(),
            'external_apis' => $this->checkExternalApis()
        ]
    ]);
});

function checkDatabase() {
    try {
        DB::connection()->getPdo();
        return ['status' => 'connected'];
    } catch (Exception $e) {
        return ['status' => 'error', 'message' => $e->getMessage()];
    }
}
```

#### Scheduled Health Checks
```php
// app/Console/Commands/HealthCheck.php
class HealthCheck extends Command
{
    protected $signature = 'app:health-check';
    protected $description = 'Run application health checks';

    public function handle()
    {
        $checks = [
            'database' => $this->checkDatabase(),
            'redis' => $this->checkRedis(),
            'storage' => $this->checkStorage(),
            'midtrans' => $this->checkMidtrans(),
            'rajaongkir' => $this->checkRajaOngkir(),
        ];

        $healthy = collect($checks)->every('status', 'ok');

        if (!$healthy) {
            Log::critical('Health check failed', $checks);
            // Send notification to admin
        }

        return $healthy ? 0 : 1;
    }
}
```

### Security Updates

#### Dependency Management
```bash
# Weekly security updates
composer audit
npm audit

# Update dependencies
composer update
npm update
```

#### Laravel Security Updates
```bash
# Update Laravel framework
composer update laravel/framework
php artisan horizon:terminate
php artisan config:cache
```

### Documentation

#### API Documentation
- **OpenAPI/Swagger**: Interactive API documentation
- **Postman Collections**: API endpoint testing
- **README files**: Setup and usage instructions

#### Technical Documentation
- **Database Schema**: Entity relationship documentation
- **Code Comments**: Inline code documentation
- **Deployment Guides**: Step-by-step deployment instructions

---

## Project Timeline & Milestones

### Phase 1: Foundation (Weeks 1-2)
- [ ] Project setup and environment configuration
- [ ] Database design and migrations
- [ ] Authentication system implementation
- [ ] Basic UI components and design system
- [ ] Admin dashboard scaffolding

### Phase 2: Core Features (Weeks 3-6)
- [ ] Product management system
- [ ] Category management
- [ ] Shopping cart functionality
- [ ] Checkout process implementation
- [ ] Midtrans payment integration

### Phase 3: Advanced Features (Weeks 7-9)
- [ ] RajaOngkir shipping integration
- [ ] User account management
- [ ] Order management system
- [ ] Admin finance module
- [ ] Email notifications

### Phase 4: Enhancement (Weeks 10-11)
- [ ] Multi-language implementation (ID/EN)
- [ ] Search and filtering
- [ ] Performance optimization
- [ ] SEO implementation
- [ ] Mobile responsiveness

### Phase 5: Testing & Deployment (Week 12)
- [ ] Comprehensive testing
- [ ] Security audit
- [ ] Performance testing
- [ ] Production deployment
- [ ] Documentation completion

---

## Budget & Resource Allocation

### Development Resources
- **Backend Developer**: 1 person, 12 weeks
- **Frontend Developer**: 1 person, 12 weeks
- **UI/UX Designer**: 1 person, 4 weeks
- **QA Tester**: 1 person, 2 weeks

### Infrastructure Costs (Monthly)
- **VPS/Dedicated Server**: $50-100
- **MySQL Database**: $20-30
- **Redis Cache**: $10-20
- **Object Storage (S3)**: $15-25
- **CDN (Cloudflare)**: $20/month
- **SSL Certificate**: Free (Let's Encrypt)
- **Monitoring Services**: $10-20

### Third-party API Costs (Monthly)
- **Midtrans**: Transaction-based (1.5-2%)
- **RajaOngkir**: Pro plan $30/month
- **Email Service**: $10-20
- **Sentry Error Tracking**: Free tier

### Estimated Total Initial Cost
- **Development**: $15,000-25,000
- **Infrastructure Setup**: $500-1,000
- **API Setup & Testing**: $200-400
- **SSL & Security**: $100-200

**Total First Year Estimate**: $20,000-30,000

---

## Risk Assessment & Mitigation

### Technical Risks

#### High Risk
- **Payment Gateway Integration**: Test extensively in sandbox
- **Database Performance**: Implement caching and optimization
- **Security Vulnerabilities**: Regular security audits

#### Medium Risk
- **Third-party API Downtime**: Implement fallback mechanisms
- **Scalability Issues**: Design for horizontal scaling
- **Mobile Compatibility**: Responsive design testing

#### Low Risk
- **Browser Compatibility**: Modern browser focus
- **Content Management**: User-friendly admin interface

### Business Risks

#### Market Competition
- **Mitigation**: Unique Korean florist positioning
- **Strategy**: Superior user experience and customer service

#### Regulatory Compliance
- **Mitigation**: Legal consultation for e-commerce regulations
- **Strategy**: Privacy policy and terms of service implementation

#### Customer Acquisition
- **Mitigation**: Digital marketing and SEO optimization
- **Strategy**: Social media integration and referral programs

---

## Conclusion

This technical specification provides a comprehensive roadmap for developing "Thejoflowers" web application. The architecture emphasizes scalability, maintainability, and user experience while adhering to modern web development best practices.

Key strengths of this technical approach:

1. **Scalable Architecture**: Laravel + Vue.js stack supports growth
2. **Modern UI/UX**: Korean aesthetic with Tailwind CSS
3. **Comprehensive Features**: Complete e-commerce functionality
4. **Multi-language Support**: ID/EN localization
5. **Secure Implementation**: Industry-standard security practices
6. **Performance Optimized**: Caching, optimization, and monitoring
7. **Production Ready**: Deployment and maintenance strategies

The specification is designed to be flexible for future enhancements while providing a solid foundation for initial deployment. Regular reviews and updates to this document will ensure alignment with evolving business requirements and technological advancements.

---

**Document Version**: 1.0
**Last Updated**: December 1, 2024
**Next Review**: January 15, 2025
**Approved By**: Technical Lead, Project Manager