# Feature: Create Supplier Order

**Feature ID:** 9
**Branch pattern:** `feature/9-create-supplier-order`
**Status:** Draft
**Created:** 2026-09-26
**Input:** Create supplier orders based on inventory needs.
**Related:** Feature 3 — Inventory Maintenance; Feature 4 — Item Maintenance; Feature 5 — Supplier Maintenance

---

## User Stories

### US-9.1: Create supplier order

**As an** office employee
**I want to** create an order for a supplier
**So that** products can be reordered when inventory is low.
**Priority:** P1
**Independent test:** Create a supplier order for a low-inventory item and verify that it is saved.
**Acceptance Scenarios:** see ### US-9.1 under Gherkin AC

### US-9.2: Calculate supplier order quantity

**As an** office employee
**I want** the system to calculate the amount to order
**So that** inventory can be brought back to the required level.
**Priority:** P1
**Independent test:** Trigger the calculation for a low-inventory item and verify the calculated quantity reaches the maximum.
**Acceptance Scenarios:** see ### US-9.2 under Gherkin AC

### US-9.3: Send supplier order

**As an** office employee
**I want to** send the supplier order
**So that** the supplier receives the order.
**Priority:** P1
**Independent test:** Send a saved supplier order and verify its status changes to Sent.
**Acceptance Scenarios:** see ### US-9.3 under Gherkin AC

---



## Functional Requirements

- **FR-001:** The system MUST identify inventory below the required minimum.
- **FR-002:** The system MUST consider quantity on hand and quantity on order.
- **FR-003:** If quantity on hand plus quantity on order is below minimum, the system MUST calculate the amount needed to reach maximum.
- **FR-004:** The calculated order quantity MUST be rounded to the nearest case quantity when case quantity is used.
- **FR-005:** A supplier order MUST identify the supplier.
- **FR-006:** A supplier order MUST identify the item and quantity ordered.
- **FR-007:** The system MUST allow an authorized employee to send the supplier order.
- **FR-008:** The system MUST keep quantity ordered separate from quantity received.

---



## Key Entities

- **Supplier Order** — Request to reorder products from a supplier.
- **Supplier** — Vendor receiving the order.
- **Item** — Product being ordered.
- **Inventory** — Current stock levels driving the reorder decision.

---



## Initial Data Model



### Supplier Order


| Field             | Type               | Rules                       |
| ----------------- | ------------------ | --------------------------- |
| supplier_order_id | String             | Required; unique            |
| supplier_id       | Supplier reference | Required                    |
| order_date        | Date               | Required                    |
| items             | Item references    | Required                    |
| quantity_ordered  | Integer            | Required; greater than zero |
| status            | String/Enum        | Draft, Sent, Received       |


---



### Inventory


| Field             | Type    | Rules                            |
| ----------------- | ------- | -------------------------------- |
| quantity_on_hand  | Integer | Zero or greater                  |
| quantity_on_order | Integer | Zero or greater                  |
| minimum_quantity  | Integer | Zero or greater                  |
| maximum_quantity  | Integer | Greater than or equal to minimum |


---



## Gherkin AC



### US-9.1 — Create supplier order



#### Scenario: Low inventory creates an order quantity

- **Given** quantity on hand plus quantity on order is below the minimum quantity
- **When** the employee creates a supplier order for the item
- **Then** the system includes the item on the supplier order



#### Scenario: Inventory does not need an order

- **Given** quantity on hand plus quantity on order is at or above the minimum quantity
- **When** the employee reviews inventory for ordering
- **Then** the system does not include the item on a supplier order



#### Scenario: Supplier order saves successfully

- **Given** a supplier and at least one item needing reorder are identified
- **When** the employee saves the supplier order
- **Then** the system saves the supplier order



#### Scenario: Supplier order does not save when supplier is missing

- **Given** no supplier is selected
- **When** the employee tries to save the supplier order
- **Then** the system does not save the supplier order



### US-9.2 — Calculate supplier order quantity



#### Scenario: Quantity on hand plus quantity on order is below minimum

- **Given** quantity on hand plus quantity on order is below the minimum quantity
- **When** the system calculates the order quantity
- **Then** the system calculates the amount needed to reach the maximum quantity



#### Scenario: Calculated amount reaches maximum

- **Given** the calculated order quantity is applied
- **When** the order is received
- **Then** quantity on hand plus quantity on order equals the maximum quantity



#### Scenario: Case quantity rounding

- **Given** the calculated order quantity does not match a whole case quantity
- **When** the system finalizes the order quantity
- **Then** the system rounds the order quantity to the nearest case quantity



### US-9.3 — Send supplier order



#### Scenario: Supplier order is sent successfully

- **Given** a supplier order has been saved with a supplier and items
- **When** the employee sends the supplier order
- **Then** the system marks the supplier order as sent

