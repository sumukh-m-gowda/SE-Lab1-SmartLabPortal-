# Lab 1 — Requirements Engineering & UML Use-Case Modelling
### Problem Statement #01: Smart Lab Equipment & Slot Reservation Portal

This repo contains the three required deliverables:

1. **`requirements.md`** — Requirements table with FR-001 to FR-005 and NFR-001, NFR-002 (ID, Type, Description, Priority, Acceptance Criteria, Rationale).
2. **`usecase_diagram.svg`** — UML use-case diagram with both actors (Student, Lab Technician), all primary use cases, at least one `«include»` relationship, and at least one `«extend»` relationship.
3. **`flow_spec_reserve_equipment_slot.md`** — 1-page use-case flow specification for the core "Reserve Equipment Slot" use case, with Preconditions, Postconditions, Main Success Scenario, and two Alternate Flows.

## Actors
- **Student** — books, views, and cancels equipment reservations.
- **Lab Technician** — checks equipment in/out, manages calibration records.

## Use cases modelled
- Authenticate User
- View Equipment Availability
- Reserve Equipment Slot *(includes Authenticate User, includes Verify Calibration Status)*
- Verify Calibration Status
- Cancel Reservation *(includes Authenticate User)*
- Check-In / Check-Out Equipment
- Apply Late-Return Penalty *(extends Check-In / Check-Out Equipment)*
- Manage Equipment Calibration
