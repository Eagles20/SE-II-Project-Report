# Feature: Receive Supplier Order
**Feature ID:** 10
**Branch pattern:** `feature/10-receive-supplier-order`
**Status:** Draft
**Created:** 2026-09-25
**Input:** Receive products ordered from suppliers and compare ordered and received quantities.
**Related:** Feature 9 — Create Supplier Order

---
## User Stories

### US-10.1: Receive supplier order
**As a** warehouse employee
**I want to** receive a supplier order
**So that** received products can be recorded.
**Priority:** P1
**Independent test:** Receive a supplier order and verify a receipt record is created.
**Acceptance Scenarios:** see ### US-10.1 under Gherkin AC

### US-10.2: Record quantity received
**As a** warehouse employee
**I want to** record quantity received
**So that** actual received inventory is known.
**Priority:** P1
**Independent test:** Enter a quantity received on a receipt and verify it is saved.
**Acceptance Scenarios:** see ### US-10.2 under Gherkin AC

### US-10.3: Identify receiving exception
**As a** warehouse manager
**I want to** compare quantity ordered with quantity received
**So that** I can see supplier receiving differences.
**Priority:** P1
**Independent test:** Create a receipt with a quantity mismatch and verify the system flags an exception.
**Acceptance Scenarios:** see ### US-10.3 under Gherkin AC

---
## Functional Requirements

- **FR-001:** The system MUST identify the supplier order being received.
- **FR-002:** The system MUST maintain quantity ordered separately from quantity received.
- **FR-003:** The system MUST record quantity received.
- **FR-004:** Quantity received MUST NOT be negative.
- **FR-005:** The system MUST compare quantity ordered and quantity received.
- **FR-006:** The system MUST identify when quantity received differs from quantity ordered.
- **FR-007:** Receiving exceptions MUST be available to management.

---
## Key Entities

- **Supplier Order** — The original order being received against.
- **Supplier Order Receipt** — Record of what was actually received for an order.
- **Item** — Product being received.
- **Supplier** — Vendor that shipped the order.

---
## Initial Data Model

### Supplier Order Receipt

| Field              | Type                      | Rules                        |
| ------------------ | -------------------------- | ------------------------------ |
| receipt_id         | String                    | Required; unique             |
| supplier_order_id  | Supplier Order reference  | Required                     |
| item_id            | Item reference            | Required                     |
| quantity_ordered   | Integer                   | From order                   |
| quantity_received  | Integer                   | Required; zero or greater    |
| received_date      | Date                       | Required                     |
| exception          | Boolean                   | True when quantities differ  |

---
## Gherkin AC

### US-10.1 — Receive supplier order

#### Scenario: Receive supplier order
- **Given** a supplier order was sent to a supplier
- **When** the employee receives the supplier order
- **Then** the system creates a supplier order receipt for the order

### US-10.2 — Record quantity received

#### Scenario: Record quantity received
- **Given** a supplier order receipt is being created
- **When** the employee enters the quantity received
- **Then** the system saves the quantity received

#### Scenario: Invalid negative quantity
- **Given** the employee enters a negative quantity received
- **When** the employee tries to save the receipt
- **Then** the system rejects the negative quantity

### US-10.3 — Identify receiving exception

#### Scenario: Received quantity equals ordered quantity
- **Given** quantity ordered is 100
- **And** quantity received is 100
- **When** the system compares the quantities
- **Then** the system does not mark the receipt as an exception

#### Scenario: Received quantity is less than ordered quantity
- **Given** quantity ordered is 100
- **And** quantity received is 80
- **When** the system compares the quantities
- **Then** the system marks the receipt as a receiving exception

#### Scenario: Received quantity is greater than ordered quantity
- **Given** quantity ordered is 100
- **And** quantity received is 110
- **When** the system compares the quantities
- **Then** the system marks the receipt as a receiving exception

#### Scenario: Receiving exception is displayed
- **Given** a receiving exception exists
- **When** the manager views receiving exceptions
- **Then** the system displays the supplier order, quantity ordered, and quantity received