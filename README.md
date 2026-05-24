# 🔧 The Tool Master BD — Inventory Management System

A complete web-based inventory and order management system built with **PHP** and **MySQL**.  
Designed for **The Tool Master BD** — managing products, tracking orders, and handling customers efficiently.

---

## 📸 Overview

| Role | Access |
|------|--------|
| 🔴 Admin | Full control — dashboard, products, orders, customers, user management, sales & inventory reports |
| 🟡 Staff | Limited access — dashboard, products, orders, customers. No access to user management, sales reports, or inventory reports |
| 🛍️ Customer | Shop, cart, order placement, own order history |

---

## 🚀 Features

### 🔐 Authentication System
- **3 user roles** — `admin`, `staff`, and `customer`
- Admin and Staff share the same `users` table with a `role` column — `ENUM('admin','staff')`
- Customers are stored in a separate `customers` table
- Single login page handles all three roles automatically
- Passwords hashed using `password_hash()` (bcrypt) — never stored as plain text
- Session-based authentication with `session_regenerate_id()` to prevent session fixation
- Role-based access control:
  - `admin` — full access to everything
  - `staff` — no access to user management, sales reports, and inventory reports
  - `customer` — redirected to shop after login
- Prepared statements on all login queries to prevent SQL injection

---

### 📦 Inventory Management
- Add, update, and delete products
- Track product **quantity** and **minimum stock level** per product
- Automatic **low stock alerts** when `quantity <= min_qty`
- **Inventory value** calculated as `SUM(price × quantity)` across all products
- Product image support with category-based emoji fallback

---

### 🧾 Order Management
- Customers can create orders from the shop or cart
- Admin can view and update **all orders**
- Customers can view **their own order history**
- **Four order statuses** with color-coded badges:
  - `pending` — amber
  - `completed` — blue
  - `delivered` — green
  - `cancelled` — red (written as text, no progress tracker shown)
- Visual **3-step progress tracker** shown on all non-cancelled orders:

| Step | Icon | Label |
|------|------|-------|
| 1 | 🧾 | Order Placed |
| 2 | ✅ | Processing |
| 3 | 🚚 | Delivered |

- Completed steps highlight in accent color, pending steps are grayed out
- If status is `cancelled`, the tracker is hidden — only the red badge is shown

---

### 📊 Admin Dashboard
The dashboard loads **8 live SQL queries** on every page load:

- Total products in inventory
- Total inventory value (`SUM(price × quantity)`)
- Total orders and pending order count
- Total revenue from `completed` and `delivered` orders only
- Total registered customers
- Low stock product count
- Recent 6 orders table
- Top 5 critically low-stock products

---

### 👤 Customer Features
- Browse all available products on the **Shop** page
- Search products by name or description
- Filter by **category**
- View individual **product detail** page
- Add to **cart** with quantity selection and stock validation
- Place orders with one click
- View full **order history**
- Visual **order progress tracker**

---

### 🎨 User Interface
- Modern responsive design — built with pure **HTML & CSS** (no frameworks)
- Clean sidebar dashboard layout for admin
- **Color-coded status badges** — amber, blue, green, red
- Alert notifications for success, warning, and error states
- Animated slideshow login page with Ken Burns effect
- Low stock warning banners on dashboard

---

### 📍 Contact & Information
- Company contact details page
- Multiple office locations
- Google Maps integration support

---

## ⚙️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | PHP (Core PHP) |
| Database | MySQL |
| Frontend | HTML, CSS |
| Server | Apache (XAMPP / Localhost) |

---

## 🛠️ How to Run This Project

### 1. Install XAMPP
Download and install XAMPP from: https://www.apachefriends.org  
Start **Apache** and **MySQL** from the XAMPP Control Panel.

### 2. Create the Database
- Open your browser and go to: `http://localhost/phpmyadmin`
- Create a new database named exactly: `inventory_db`

### 3. Import the Database
- Select `inventory_db` in phpMyAdmin
- Click **Import** → choose the `database.sql` file from the project → click **Go**

### 4. Set Up the Project Folder
Move the project folder to:
```
C:\xampp\htdocs\inventory_project
```

### 5. Run the Project
Open your browser and visit:
```
http://localhost/inventory_project
```

---

## 📥 Clone the Repository

```bash
git clone https://github.com/ArefinRonok/inventory_project.git
```

---

## 🔒 Security Practices

- `password_hash()` with `PASSWORD_DEFAULT` (bcrypt) for storing passwords
- `password_verify()` for login — raw passwords never compared directly
- Prepared statements with `bind_param()` on all user-input queries
- `htmlspecialchars()` on all output to prevent XSS
- `session_regenerate_id(true)` after login to prevent session fixation
- Login-protected pages redirect to `login.php` if no valid session exists

---

## 📁 Project Structure

```
inventory_project/
├── admin/              # Admin-only pages
├── customer/           # Customer-facing pages
├── includes/           # Shared CSS stylesheets
├── uploads/            # Product images
├── db.php              # Database connection (shared via require)
├── layout.php          # Admin sidebar layout (included by all admin pages)
├── nav.php             # Customer navbar (included by all customer pages)
├── login.php           # Unified login for admin & customers
├── logout.php          # Session destroy
├── dashboard.php       # Admin dashboard
├── products.php        # Product list & management
├── add_product.php     # Add / edit products
├── orders.php          # Order management
├── customers.php       # Customer list
├── shop.php            # Customer shop page
├── product.php         # Product detail page
├── cart.php            # Shopping cart
├── index.php           # Home page
└── database.sql        # Full database schema & seed data
```

---

## 👨‍💻 Author

**ArefinRonok**  
GitHub: [@ArefinRonok](https://github.com/ArefinRonok)

---

*© 2025 The Tool Master BD. Built with Core PHP & MySQL.*
