# Thrift Store E-Commerce — ER Diagram

A database design for an Instagram-based thrift and handmade products store.

---

## ER Diagram

![Thrift Store ER Diagram](https://drive.google.com/uc?export=view&id=1log5MDu40VOyDBiL5iovJhf5iVQqwqVL)

> If the image does not load, [click here to view it on Google Drive](https://drive.google.com/file/d/1log5MDu40VOyDBiL5iovJhf5iVQqwqVL/view?usp=sharing)

---

## Business Context

A small creator runs an Instagram-based store selling:
- **Thrifted items** — unique pieces, only one available per item
- **Handmade products** — can have multiple units in different sizes or colours

Orders were initially managed through Instagram DMs and WhatsApp. As the business grew, a proper database was needed to manage products, orders, payments, and deliveries.

---

## Entities

| Entity | Description |
|---|---|
| `customers` | Stores customer contact and address details |
| `products` | Stores all product info including type, stock, price |
| `orders` | Represents a single order placed by a customer |
| `order_details` | Junction table — links products to orders |
| `payments` | Tracks payment method, status and amount |
| `delivery_status` | Tracks shipping and delivery progress |

---

## Relationships

- A **customer** can place multiple **orders** (one to many)
- An **order** can contain multiple **products** (many to many via `order_details`)
- Each **order** has one **payment** record (one to one)
- Each **order** has one **delivery** record (one to one)

---

## Key Design Decisions

- `isThrifted (boolean)` on Product distinguishes thrifted vs handmade items
- `condition` is **nullable** — applies to thrifted items only, not handmade
- `pricePerUnit` is stored in `order_details` not on Product, to preserve historical pricing
- `deliveryAddress` is stored on `delivery_status` not on Customer, to support different addresses per order
- Payment and Delivery records are created **after** the Order, using `orderId` as FK — avoids circular dependency

---

## Tools Used

- [Eraser.io](https://eraser.io) — for ER diagram design
