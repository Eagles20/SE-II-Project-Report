# Feature: Receive Customer Order

**Feature ID:** 12
**Branch pattern:** `feature/12-receive-customer-order`
**Status:** Draft
**Created:** 2026-09-25
**Input:** Receive customer orders for products from the warehouse.
**Depends on:** [Feature 6 — Customer Maintenance](feature-6-customer-maintenance.md); [Feature 8 — Customer Order Form Maintenance](feature-8-customer-order-form-maintenance.md)

---

## User Stories

### US-12.1: Receive customer order

**As an** office employee
**I want to** receive a customer order
**So that** the warehouse knows what the customer requested.
**Priority:** P1
**Independent test:** Receive a customer order and verify it is saved.
**Acceptance Scenarios:** see ### US-12.1 under Gherkin AC

### US-12.2: Record ordered items

**As an** office employee
**I want to** record the items and quantities ordered
**So that** the order can be picked correctly.
**Priority:** P1
**Independent test:** Add ordered items with quantities and verify they are saved.
**Acceptance Scenarios:** see ### US-12.2 under Gherkin AC

### US-12.3: Confirm customer order

**As an** office employee
**I want to** confirm the customer order
**So that** it can move to picking.
**Priority:** P1
**Independent test:** Confirm a complete customer order and verify its status moves to Picking.
**Acceptance Scenarios:** see ###  US-12.3 under Gherkin AC

---



## Functional Requirements

- **FR-001:** The system MUST identify the customer.
- **FR-002:** The system MUST identify each ordered item.
- **FR-003:** The system MUST maintain quantity ordered separately from quantity picked.
- **FR-004:** Quantity ordered MUST be greater than zero.
- **FR-005:** The system MUST allow a received customer order to move to picking after required information is complete.
- **FR-006:** The system MUST reject an order without a customer.
- **FR-007:** The system MUST reject an order without ordered items.

---



## Key Entities

- **Customer Order** — Order received from a customer for products.
- **Customer** — Customer placing the order.
- **Item** — Product requested on the order.

---



## Initial Data Model



### Customer Order


| Field             | Type               | Rules                                 |
| ----------------- | ------------------ | ------------------------------------- |
| customer_order_id | String             | Required; unique                      |
| customer_id       | Customer reference | Required                              |
| order_date        | Date               | Required                              |
| status            | String/Enum        | Received, Picking, Shipped, Delivered |


---



### Customer Order Item


| Field             | Type                     | Rules                       |
| ----------------- | ------------------------ | --------------------------- |
| customer_order_id | Customer Order reference | Required                    |
| item_id           | Item reference           | Required                    |
| quantity_ordered  | Integer                  | Required; greater than zero |


---



## Gherkin AC



### US-12.1 — Receive customer order



#### Scenario: Receive order successfully

- **Given** a customer and at least one item are identified
- **When** the employee receives the customer order
- **Then** the system saves the customer order



#### Scenario: Missing customer

- **Given** no customer is selected
- **When** the employee tries to receive the customer order
- **Then** the system rejects the order



### US-12.2 — Record ordered items



#### Scenario: Missing item

- **Given** no item is added to the order
- **When** the employee tries to receive the customer order
- **Then** the system rejects the order



#### Scenario: Invalid quantity

- **Given** the employee enters a quantity ordered of zero or less
- **When** the employee tries to save the customer order
- **Then** the system rejects the invalid quantity



### US-12.3 — Confirm customer order



#### Scenario: Confirm complete order

- **Given** a customer order has a customer and valid ordered items
- **When** the employee confirms the customer order
- **Then** the system moves the customer order to picking



#### Scenario: Incomplete order cannot move to picking

- **Given** a customer order is missing required information
- **When** the employee tries to confirm the customer order
- **Then** the system does not move the customer order to picking

