# Feature: Routes

**Feature ID:** 6

**Branch pattern:** `feature/6-routes`

**Status:** Draft

**Created:** 2026-10-02

**Input:** Church staff can record who needs a ride to church, see the pickup address and needs, and make routes for drivers.

**Depends on:** [Feature-1 user authentication and management](<Feature-1 user authentication and management.md>), [Feature-2 member management](<Feature-2 member management.md>)

---

## User Stories

### US-6.1: Ask for a ride for a member
**As a** church admin

**I want to** record that a member needs a ride, with the pickup address and any special needs

**So that** the church knows who needs a ride and where to go.

**Priority:** P1

**Independent test:** The admin creates a ride request and it shows in the list for the service.

**Acceptance scenarios:** see ### US-6.1 under Gherkin AC

### US-6.2: See who needs a ride
**As a** church admin

**I want to** see all ride requests for a service with address, phone, passengers and notes

**So that** I know everyone who needs a ride.

**Priority:** P1

**Independent test:** The admin opens a service and sees each request with its details.

**Acceptance scenarios:** see ### US-6.2 under Gherkin AC

### US-6.3: Create a route and choose a driver
**As a** church admin

**I want to** create a route for a service, choose a driver and add ride requests

**So that** every person who needs a ride has a driver.

**Priority:** P1

**Independent test:** The admin creates a route with a driver and adds requests to it.

**Acceptance scenarios:** see ### US-6.3 under Gherkin AC

### US-6.4: Order the stops and see the route
**As a** driver

**I want to** see the stops of my route in order, with address, phone, passengers and notes

**So that** I know where to go and who to pick up.

**Priority:** P1

**Independent test:** The admin sets the order of the stops and the route shows them in that order.

**Acceptance scenarios:** see ### US-6.4 under Gherkin AC

### US-6.5: Update a pickup
**As a** driver

**I want to** mark a stop as picked up, not found or cancelled

**So that** everyone knows who still needs a ride.

**Priority:** P2

**Independent test:** The user marks a stop as picked up and its status changes.

**Acceptance scenarios:** see ### US-6.5 under Gherkin AC

### US-6.6: Edit or cancel a ride request
**As a** church admin

**I want to** change a ride request, move it to another route, or cancel it

**So that** the routes stay correct when plans change.

**Priority:** P2

**Independent test:** The admin moves a request to another route and both routes change.

**Acceptance scenarios:** see ### US-6.6 under Gherkin AC

### US-6.7: Open an address in a maps app
**As a** driver

**I want to** open a pickup address in a maps app

**So that** I can get directions.

**Priority:** P3

**Independent test:** The driver clicks a stop and the address opens in a maps app.

**Acceptance scenarios:** see ### US-6.7 under Gherkin AC

---

## Functional Requirements

- **FR-001**: System MUST let a logged-in user create a ride request for a member and a service.
- **FR-002**: System MUST ask for a pickup address and MUST fill it in from the member's address when there is one.
- **FR-003**: System MUST NOT allow two active ride requests for the same member and service.
- **FR-004**: System MUST let the user save the number of passengers and a note about special needs.
- **FR-005**: System MUST show all ride requests of a service: name, address, phone, passengers, note and status.
- **FR-006**: System MUST let the user filter the requests that are not on a route.
- **FR-007**: System MUST let the user create a route with a name, a driver (a member) and the number of seats.
- **FR-008**: System MUST let the user add a ride request to a route. A request can be on only one route.
- **FR-009**: System MUST NOT allow more passengers on a route than seats.
- **FR-010**: System MUST let the user set the order of the stops and show the stops in that order.
- **FR-011**: System MUST let the user change the status of a stop: picked up, not found or cancelled.
- **FR-012**: System MUST let the user edit, move or cancel a ride request.
- **FR-013**: System SHOULD give a link to open a pickup address in a maps app.
- **FR-014**: System MUST require a login (Feature 1) for all ride and route actions.

---

## Initial Data Model

Services come from Feature 1 and members come from Feature 2. The system keeps two things:

- **Ride requests:** which service, which member, the pickup address (required, filled in from the member's address), the number of passengers (at least 1), special needs (optional), and the status (requested, assigned, picked up, not found or cancelled). A request can also have a route and a stop order. A member can have only one active request for each service.
- **Routes:** which service, a name (for example "North route"), the driver (one member), and the number of seats.

---

## Gherkin AC

### US-6.1 — Ask for a ride for a member

#### Scenario: Ask for a ride
* **Given** a service and a member exist
* **When** the admin creates a ride request with the pickup address and the number of passengers
* **Then** the system saves the request
* **And** it shows in the list for the service

#### Scenario: Address filled in
* **Given** the member has an address
* **When** the admin starts a ride request for the member
* **Then** the system fills in the pickup address from the member's address

#### Scenario: Address missing
* **Given** the admin is creating a ride request
* **When** the admin saves without a pickup address
* **Then** the system does not save the request
* **And** the system says the address is needed

#### Scenario: Request already exists
* **Given** the member already has an active request for the service
* **When** the admin creates another request for the same member and service
* **Then** the system does not create it
* **And** the system says a request already exists

### US-6.2 — See who needs a ride

#### Scenario: See the requests
* **Given** ride requests exist for a service
* **When** the admin opens the requests of the service
* **Then** the system shows the name, address, phone, passengers, note and status of each request

#### Scenario: Requests without a route
* **Given** some requests are on a route and some are not
* **When** the admin filters by "no route"
* **Then** the system shows only the requests that are not on a route

### US-6.3 — Create a route and choose a driver

#### Scenario: Create a route
* **Given** the admin is creating a route for a service
* **When** the admin enters a name, picks a driver and enters the seats
* **Then** the system creates the route

#### Scenario: Add a request to a route
* **Given** a route and a request without a route exist
* **When** the admin adds the request to the route
* **Then** the request shows on the route
* **And** the request is not shown as "no route" anymore

#### Scenario: Route is full
* **Given** a route has fewer seats than the passengers of a request
* **When** the admin adds the request to the route
* **Then** the system does not add it
* **And** the system says there are not enough seats

### US-6.4 — Order the stops and see the route

#### Scenario: Set the order
* **Given** a route has several stops
* **When** the admin changes the order of the stops
* **Then** the system saves the new order

#### Scenario: See the route
* **Given** a route has stops in order
* **When** the user opens the route
* **Then** the system shows the stops in order
* **And** each stop shows the address, phone, passengers and note

### US-6.5 — Update a pickup

#### Scenario: Picked up
* **Given** a stop is on a route
* **When** the user marks it as picked up
* **Then** the status of the stop is "picked up"

#### Scenario: Not found
* **Given** a stop is on a route
* **When** the user marks it as not found
* **Then** the status of the stop is "not found"
* **And** the stop stays on the route

### US-6.6 — Edit or cancel a ride request

#### Scenario: Change the address
* **Given** a ride request exists
* **When** the admin changes the pickup address and saves
* **Then** the route shows the new address

#### Scenario: Cancel a request
* **Given** a request is on a route
* **When** the admin cancels it and confirms
* **Then** the request is cancelled
* **And** the seats on the route are free again

### US-6.7 — Open an address in a maps app

#### Scenario: Open the address
* **Given** the user is looking at a route
* **When** the user clicks the map link of a stop
* **Then** the address opens in a maps app
