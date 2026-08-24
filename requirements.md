# Requirements Table — Smart Lab Equipment & Slot Reservation Portal

**Actors:** Student, Lab Technician

## Functional Requirements

| ID | Type | Description | Priority | Acceptance Criteria | Rationale |
|---|---|---|---|---|---|
| FR-001 | Functional | The system shall allow authenticated students to view real-time availability and reserve a maximum 2-hour slot for any calibrated equipment up to 7 days in advance. | High | **Pass:** Slot is successfully locked and reservation token generated. **Fail:** Double-booking allowed or reservation exceeds 2-hour limit. | Prevents scheduling conflicts on high-value shared hardware and gives students predictable access. |
| FR-002 | Functional | The system shall verify equipment calibration status at the time of reservation and block booking of any instrument overdue for calibration. | High | **Pass:** Reservation attempt on an overdue instrument is rejected with an explanatory message. **Fail:** An overdue instrument is successfully reserved. | Ensures experimental results are valid and protects students from using out-of-spec instruments. |
| FR-003 | Functional | The system shall allow a lab technician to record equipment check-out at slot start and check-in at return, logging the actual return timestamp against the reservation. | Medium | **Pass:** Check-in timestamp is stored and linked to the correct reservation ID. **Fail:** Return is not logged or is linked to the wrong reservation. | Creates an auditable record of equipment custody and enables late-return detection. |
| FR-004 | Functional | The system shall automatically flag a reservation as "late" if equipment is checked in after the slot end time, and apply a 24-hour booking suspension to the student's account. | High | **Pass:** Late check-in triggers a suspension flag on the student profile. **Fail:** Late return is logged but no penalty is applied. | Enforces fair, disciplined use of limited lab resources. |
| FR-005 | Functional | The system shall allow a student to cancel a confirmed reservation up to 1 hour before the slot start time, releasing the slot for other students. | Medium | **Pass:** Cancelled slot immediately reappears as available. **Fail:** Slot remains locked after cancellation, or cancellation is allowed within the 1-hour window. | Improves equipment utilization by freeing unused slots quickly. |

## Non-Functional Requirements

| ID | Type | Description | Priority | Acceptance Criteria | Rationale |
|---|---|---|---|---|---|
| NFR-001 | Performance & Security | The system shall ensure that concurrent slot reservation requests are processed within 200 ms with strict database-level lock isolation to prevent race conditions. | High | **Pass:** Benchmarking tests confirm target latency and security standards under simulated peak load. | High-value equipment is scarce; race conditions during peak enrollment periods must not cause conflicting bookings. |
| NFR-002 | Availability & Usability | The system shall maintain 99.5% uptime during lab operating hours (8 AM–8 PM) and render correctly on mobile devices with screen widths ≥360px. | Medium | **Pass:** Uptime monitoring logs meet the 99.5% threshold; UI passes responsive layout checks on target devices. | Students frequently check slot availability from phones between classes; downtime directly blocks lab access. |
