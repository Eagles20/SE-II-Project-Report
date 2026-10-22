# Feature: Ref Payment

**Feature ID:** 13  
**Branch pattern:** `feature/13-ref-payment`  
**Status:** Draft  
**Created:** 2026-10-21  
**Input:** Track what is owed to each ref and mark games as paid.  
**Depends on:** [Feature 5-Maintain-Game](Feature-5-Maintain-Game.md), [Feature 9-Maintain-Ref](Feature-9-Maintain-Ref.md)

------

## User Stories

### US-13.1: See amount owed

**As an** owner  
**I want to** see how much I owe each ref and in total  
**So that** I pay the right amount.  
**Priority:** P1  
**Independent test:** Open the pay page and verify that the amount owed is correct.  
**Acceptance Scenarios:** see ### US-13.1 under Gherkin AC

### US-13.2: Mark games as paid

**As an** owner  
**I want to** mark one or many games as paid with a date and a method  
**So that** I have a record of what I paid.  
**Priority:** P1  
**Independent test:** Mark games as paid and verify that the amount owed goes down.  
**Acceptance Scenarios:** see ### US-13.2 under Gherkin AC

### US-13.3: Change the pay of one game

**As an** owner  
**I want to** change the pay of one game  
**So that** special cases like a bonus are correct.  
**Priority:** P2  
**Independent test:** Change a pay amount and verify the new amount owed.  
**Acceptance Scenarios:** see ### US-13.3 under Gherkin AC

### US-13.4: Undo a paid mark

**As an** owner  
**I want to** undo a paid mark with a reason  
**So that** I can fix a mistake.  
**Priority:** P2  
**Independent test:** Undo a paid mark and verify that the history keeps the reason.  
**Acceptance Scenarios:** see ### US-13.4 under Gherkin AC

### US-13.5: Set pay rule for cancelled games

**As an** owner  
**I want to** choose if a cancelled game is paid or not  
**So that** I can follow my own rule.  
**Priority:** P3  
**Independent test:** Cancel a game and choose Do not pay, then verify the amount owed.  
**Acceptance Scenarios:** see ### US-13.5 under Gherkin AC

### US-13.6: Pay report

**As an** owner  
**I want to** build a pay report for a date range and filter payments  
**So that** I can check my costs.  
**Priority:** P2  
**Independent test:** Build a report for a date range and verify the totals.  
**Acceptance Scenarios:** see ### US-13.6 under Gherkin AC

### US-13.7: Export report

**As an** owner  
**I want to** export the pay report to a CSV file  
**So that** I can keep it or use it in a spreadsheet.  
**Priority:** P3  
**Independent test:** Export a report and verify the CSV content.  
**Acceptance Scenarios:** see ### US-13.7 under Gherkin AC

### US-13.8: View my pay

**As a** ref  
**I want to** see my games with the pay, my pay history and my unpaid total  
**So that** I know what I will receive and what I was paid.  
**Priority:** P1  
**Independent test:** Log in as a ref and verify that only own pay is shown.  
**Acceptance Scenarios:** see ### US-13.8 under Gherkin AC

### US-13.9: Keep pay private

**As a** person from the public  
**I want to** not see ref pay  
**So that** ref money information stays private.  
**Priority:** P1  
**Independent test:** Open public pages and verify that no ref pay is shown.  
**Acceptance Scenarios:** see ### US-13.9 under Gherkin AC

-----

## Functional Requirements

- **FR-001:** The system MUST give every ref assignment a pay amount that starts from the ref's pay rate.
- **FR-002:** The system MUST show the owner the amount owed to each ref (all unpaid games) and the total owed to all refs.
- **FR-003:** The system MUST let the owner change the pay of one assignment (for example a bonus).
- **FR-004:** The system MUST let the owner mark one or many assignments as paid, and MUST save the pay date and the payment method (cash, check, other).
- **FR-005:** The system MUST let the owner undo a paid mark. The system MUST ask for a reason and MUST keep a history.
- **FR-006:** The system MUST let the owner choose Pay or Do not pay for a cancelled game.
- **FR-007:** The system MUST let the owner filter payments by ref, season, date range and paid or unpaid.
- **FR-008:** The system MUST build a pay report for a date range and MUST let the owner export it to a CSV file.
- **FR-009:** The pay report MUST include the start date and the end date (both days included) and MUST use the league's local time zone (America/Chicago).
- **FR-010:** When a report or a filter finds nothing, the system MUST show "No payments found" and amounts of 0, and MUST NOT show an error.
- **FR-011:** The system MUST let a ref see only their own games, pay and pay history.
- **FR-012:** The system MUST NOT show ref pay on the public pages.
- **FR-013:** The system MUST let the owner use this feature (main user: owner), and MUST let a ref only view their own payments.
- **FR-014:** The system MUST work on an office computer and on a phone.

-----

## Key Entities

- **Ref payment** — The pay amount and paid status of one ref assignment.
- **Payment history** — The record of paid marks and undo actions.

-----

## Initial Data Model

### Ref payment

- assignment_id: String — Required, unique
- ref_id: String — Required
- game_id: String — Required
- pay_amount: Decimal — Required
- is_paid: Boolean — Required
- paid_date: Date — Optional
- payment_method: String — Optional (Cash, Check, Other)
- pay_cancelled_game: Boolean — Optional

### Payment history

- history_id: String — Required, unique
- assignment_id: String — Required
- action: String — Required (Paid, Undo)
- reason: String — Optional, required for Undo
- changed_by: String — Required
- changed_at: DateTime — Required

-----

## Gherkin AC

### US-13.1 — See amount owed

#### Scenario: Amount owed is displayed

- **Given** Paul worked 4 games at 30 each and none are paid
- **When** the owner opens Paul's pay page
- **Then** the system shows 120 owed

#### Scenario: Total owed is displayed

- **Given** two refs have unpaid games
- **When** the owner opens the pay summary
- **Then** the system shows the total owed to all refs

#### Scenario: Wrong role cannot see all pay

- **Given** a manager is signed in
- **When** the manager tries to open the pay page
- **Then** the system rejects the request

### US-13.2 — Mark games as paid

#### Scenario: Games are marked as paid

- **Given** Paul has 4 unpaid games at 30 each
- **When** the owner marks 2 games as paid by cash
- **Then** Paul is owed 60
- **And** the 2 games show the pay date and "Cash"

#### Scenario: Payment method is required

- **Given** the owner marks a game as paid
- **When** no payment method is chosen
- **Then** the system does not save the paid mark

### US-13.3 — Change the pay of one game

#### Scenario: Pay is changed

- **Given** a game pays 30
- **When** the owner changes the pay to 40 for that game
- **Then** Paul is owed 40 for that game

### US-13.4 — Undo a paid mark

#### Scenario: Paid mark is undone

- **Given** a game is marked paid by mistake
- **When** the owner undoes it with a reason
- **Then** the game is unpaid again
- **And** the history keeps the reason

#### Scenario: Undo without a reason fails

- **Given** a game is marked paid
- **When** the owner tries to undo it without a reason
- **Then** the system does not undo the paid mark

### US-13.5 — Set pay rule for cancelled games

#### Scenario: Cancelled game is not paid

- **Given** a game was cancelled and the owner chooses "Do not pay"
- **When** the owner opens Paul's pay page
- **Then** that game adds 0 to the amount owed

#### Scenario: Cancelled game is paid

- **Given** a game was cancelled and the owner chooses "Pay"
- **When** the owner opens Paul's pay page
- **Then** that game adds its pay to the amount owed

### US-13.6 — Pay report

#### Scenario: Report is displayed

- **Given** refs have games in October
- **When** the owner builds the report for October
- **Then** the system shows each ref, game, date, pay and status

#### Scenario: Filter by unpaid

- **Given** some games are paid and some are not
- **When** the owner filters by unpaid
- **Then** the system shows only unpaid games

#### Scenario: End date is included

- **Given** Paul has a game on Oct 31
- **When** the owner builds the report from Oct 1 to Oct 31
- **Then** the report includes the Oct 31 game

#### Scenario: Empty report

- **Given** no games were worked in the date range
- **When** the owner builds the report
- **Then** the system shows "No payments found" and a total of 0

### US-13.7 — Export report

#### Scenario: Report is exported

- **Given** a pay report is shown
- **When** the owner exports it
- **Then** the system gives a CSV file with ref, game, date, pay and status

### US-13.8 — View my pay

#### Scenario: Ref sees only own pay

- **Given** Paul is signed in
- **When** Paul opens the payments page
- **Then** the system shows only Paul's games and pay

#### Scenario: Ref sees unpaid total

- **Given** Paul has 2 unpaid games at 30 each
- **When** Paul opens the payments page
- **Then** the system shows 60 unpaid

### US-13.9 — Keep pay private

#### Scenario: Pay is hidden from the public

- **Given** a person is not logged in
- **When** the person opens any public page
- **Then** the system does not show ref pay
