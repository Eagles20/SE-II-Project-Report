# Feature: Language Selection

**Feature ID:** 7

**Branch pattern:** `feature/7-language-selection`

**Status:** Draft

**Created:** 2026-10-02

**Input:** People can use the church member system in English or Spanish.

**Depends on:** [Feature-1 user authentication and management](<Feature-1 user authentication and management.md>)

---

## User Stories

### US-7.1: Choose a language
**As a** user

**I want to** choose English or Spanish

**So that** I can use the system in the language I know best.

**Priority:** P1

**Independent test:** The user picks a language and the system shows its text in that language.

**Acceptance scenarios:** see ### US-7.1 under Gherkin AC

### US-7.2: Remember my language
**As a** logged-in user

**I want to** have the system remember my language

**So that** I do not need to choose it every time I log in.

**Priority:** P2

**Independent test:** The user picks Spanish, logs out, logs in again, and the system is still in Spanish.

**Acceptance scenarios:** see ### US-7.2 under Gherkin AC

### US-7.3: Start in a default language
**As a** new user

**I want to** have the system start in a default language

**So that** I can use it right away.

**Priority:** P3

**Independent test:** A user who never chose a language sees the system in English.

**Acceptance scenarios:** see ### US-7.3 under Gherkin AC

---

## Functional Requirements

- **FR-001**: System MUST support English and Spanish.
- **FR-002**: System MUST let the user change the language on every page, also on the login page.
- **FR-003**: System MUST show menus, labels, buttons and messages in the chosen language.
- **FR-004**: System MUST save the language of a logged-in user and use it at the next login.
- **FR-005**: System MUST use English when the user did not choose a language.
- **FR-006**: System MUST NOT translate information typed by users, like names, addresses, topics and notes.

---

## Initial Data Model

The system keeps two small things:

- **Preferred language:** one more field for each user (Feature 1): English (`en`) or Spanish (`es`). The default is English.
- **Language texts:** the English and Spanish version of each menu, label, button and message. These are app settings, not a database table.

---

## Gherkin AC

### US-7.1 — Choose a language

#### Scenario: Use Spanish
* **Given** the system is in English
* **When** the user picks Spanish
* **Then** the system shows its text in Spanish

#### Scenario: Use English
* **Given** the system is in Spanish
* **When** the user picks English
* **Then** the system shows its text in English

#### Scenario: Change language before login
* **Given** the user is on the login page
* **When** the user picks Spanish
* **Then** the login page is in Spanish

#### Scenario: Typed information
* **Given** the system is in Spanish
* **When** the user opens a member's details
* **Then** the name and address show exactly as they were typed

### US-7.2 — Remember my language

#### Scenario: Language is remembered
* **Given** the user picked Spanish and logged out
* **When** the user logs in again
* **Then** the system is in Spanish

### US-7.3 — Start in a default language

#### Scenario: Default language
* **Given** the user never chose a language
* **When** the user opens the system
* **Then** the system is in English
