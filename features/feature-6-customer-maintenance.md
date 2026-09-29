# Feature: Customer Maintenance

**Feature ID:** 6
**Branch pattern:** `feature/6-customer-maintenance`
**Status:** Draft
**Created:** 2026-09-25
**Input:** Maintain customer information for wholesale customers. 
**Depends on:** Feature 1 — Company Maintenance

---

## User Stories

### US-6.1: Add customer

**As an** office employee
**I want to** add a customer
**So that** the warehouse can maintain customer information.
**Priority:** P1
**Independent test:** Add a customer and verify that it is saved.
**Acceptance Scenarios:** see US-6.1 under Gherkin AC

### US-6.2: Edit customer

**As an** office employee
**I want to** edit customer information
**So that** customer information stays accurate.
**Priority:** P1
**Independent test:** Edit a customer and verify that the change is saved.
**Acceptance Scenarios:** see US-6.2 under Gherkin AC

### US-6.3: Delete customer

**As an** office employee
**I want to** delete a customer
**So that** incorrect customer information can be removed.
**Priority:** P1
**Independent test:** Delete a customer and verify that it is no longer active.
**Acceptance Scenarios:** see US-6.3 under Gherkin AC

### US-6.4: View customer

**As an** office employee
**I want to** view customer information
**So that** I can see the customer's information.
**Priority:** P1
**Independent test:** Open a customer and verify the current information is displayed.
**Acceptance Scenarios:** see US-6.4 under Gherkin AC

---



## Functional Requirements

- **FR-001:** The system MUST maintain customers.
- **FR-002:** Each customer MUST have a unique customer identifier.
- **FR-003:** Customer name MUST be required.
- **FR-004:** Customer address MUST be maintained.
- **FR-005:** Customer phone MUST be maintained.
- **FR-006:** Customer email MAY be maintained.
- **FR-007:** The system MUST allow authorized users to add, edit, delete, and view customers.
- **FR-008:** The system MUST reject duplicate customer identifiers.

---



## Key Entities

- **Customer** — A retail or convenience-store customer who purchases products from the warehouse.



## Initial Data Model



### Customer


| Field       | Type   | Rules            |
| ----------- | ------ | ---------------- |
| customer_id | String | Required; unique |
| name        | String | Required         |
| address     | String | Required         |
| phone       | String | Required         |
| email       | String | Optional         |


---



## Gherkin AC



### US-6.1 — Add customer



#### Scenario: Customer is added successfully

- **Given** a customer does not already exist
- **When** the employee enters the required customer information and saves
- **Then** the system saves the customer



#### Scenario: Customer is not saved due to missing information

- **Given** a customer is being added
- **When** required customer information is missing
- **Then** the system does not save the customer



#### Scenario: Duplicate customer is rejected

- **Given** a customer with the same identifier already exists
- **When** the employee tries to add a customer with that identifier
- **Then** the system rejects the duplicate customer



### US-6.2 — Edit customer



#### Scenario: Customer is edited successfully

- **Given** a customer exists
- **When** the employee changes customer information and saves
- **Then** the system saves the updated customer



#### Scenario: Customer edit fails

- **Given** a customer exists
- **When** required information is removed during edit
- **Then** the system does not save the update



### US-6.3 — Delete customer



#### Scenario: Customer is deleted successfully

- **Given** a customer exists
- **When** the employee deletes the customer
- **Then** the system removes the customer from active records



#### Scenario: Delete unknown customer fails

- **Given** the customer does not exist
- **When** the employee tries to delete it
- **Then** the system rejects the delete operation



### US-6.4 — View customer



#### Scenario: Customer information is displayed

- **Given** a customer exists
- **When** the employee views the customer
- **Then** the system displays the customer information

