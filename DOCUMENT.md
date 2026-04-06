# Instagram Thrift Creator Store – ER Diagram

## Overview

This project represents a **database design (ER Diagram)** for a small Instagram-based thrift and handmade product store.

The system is designed to handle:

* Product management (thrift + handmade)
* Inventory tracking
* Customer orders
* Payment status
* Shipping details

---

## Business Problem

Initially, the store handled orders via Instagram DMs and WhatsApp. As the business grew, the owner needed a structured way to:

* Track products and their availability
* Manage customer orders
* Store customer details
* Handle payments and shipping

This ERD provides a scalable solution for these requirements.

---

## Entities and Their Purpose

### Customers

Stores bassic customer information.

**Fields:**

* id (PK)
* name
* phone
* email

---

### Customer Details

Stores extended address information for customers.

**Fields:**

* id (PK)
* customer_id (FK → customers.id)
* address
* city
* pincode
* country

---

### Categories

Used to group products logically (e.g., Clothing, Accessories).

**Fields:**

* id (PK)
* name

---

### Products

Represents the main product.

**Fields:**

* id (PK)
* name
* description
* price
* product_type (thrift / handmade)
* category_id (FK → categories.id)

---

### Product Variants

Handles variations like size, color, and condition.

**Fields:**

* id (PK)
* product_id (FK → products.id)
* size
* color
* condition
* price (variant-specific)

---

### Inventory

Track available stock for each variant.

**Fields:**

* id (PK)
* variant_id (FK → product_variants.id)
* quantity
* updated_at

👉 For thrift item → quantity = 1
👉 For handmade items → quantity > 1

---

### Orders

Represents a customer order.

**Fields:**

* id (PK)
* customer_id (FK → customers.id)
* order_date
* total_amount
* status (placed, cancelled, completed)

---

### Order Items

Junction table connecting orders and product variants.

**Fields:**

* id (PK)
* order_id (FK → orders.id)
* variant_id (FK → product_variants.id)
* quantity
* price_at_purchase

---

### 💳 Payments

Stores payment details for an order.

**Fields:**

* id (PK)
* order_id (FK → orders.id)
* status (paid, pending, failed)
* methods (UPI, card, etc.. )
* payment_date

---

### 🚚 Shipping

Tracks delivery status of an order.

**Fields:**

* id (PK)
* order_id (FK → orders.id)
* status (shipped, delivered)
* tracking_number
* delivery_date

---

## Relationshipss

* One customer can place multiple orders
* One order can contain multiple products (via order_items)
* One product can have multiple variants
* Each variant has its own inventory
* Each order has one payment and one shipping record
* Products belong to categories

---

## Key Design Decisions

### Product Variants

Instead of storing size/color directly in products, a separate table is used:

* Supports multiple variations
* Keeps design normalized

---

### 🔹 Order Items (Junction Table)

Handles many-to-many relationship:

* One order → multiple products
* One product → multiple orders

---

### 🔹 Inventory Separation

Inventory is managed per variant:

* Allow accurate stock tracking
* Supports both thrift and handmade logic

---

### 🔹 Price Snapshot

`price_at_purchase` ensures:

* Order history remains accurate even if product price changes later

---

## Tools Used

* ER Diagram created using **Eraser**
* DBML-style schema for structure

---

## Conclusion

This ER diagram provides a **clean, normalized, and scalable database design** for a growiing thrift and handmade product business.

It ensures:

* Proper data organization
* Efficient querying
* Real-world applicability

---

## 👨‍💻 Author

Debashis Das
