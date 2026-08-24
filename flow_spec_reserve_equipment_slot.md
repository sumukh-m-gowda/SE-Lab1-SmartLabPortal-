# Use-Case Flow Specification

## Use Case: Reserve Equipment Slot

**Primary Actor:** Student
**Supporting Actors:** Lab Technician (equipment/calibration data owner)
**Related Requirements:** FR-001, FR-002, NFR-001

### Brief Description
A student books a time slot on a specific piece of calibrated lab equipment (oscilloscope, logic analyzer, or FPGA board), for up to 2 hours, up to 7 days in advance. The system checks calibration status and slot availability before confirming the booking.

### Preconditions
1. The student has a valid, authenticated account on the portal.
2. The requested equipment exists in the system's inventory.
3. The student has no active booking suspension (see FR-004).

### Postconditions
**Success:** A reservation record is created and locked against the equipment/time-slot pair; a unique reservation token is generated and shown to the student; the slot no longer appears as available to other students.
**Failure:** No reservation record is created; the equipment/time-slot pair remains unchanged and available (if it was available before the attempt).

### Main Success Scenario
1. The student logs into the portal *(include: Authenticate User)*.
2. The student navigates to the equipment catalogue and selects an instrument (e.g., "Oscilloscope – Bay 3").
3. The system displays real-time availability for that instrument over the next 7 days.
4. The student selects an open slot of up to 2 hours.
5. The system verifies the equipment's calibration status *(include: Verify Calibration Status)*.
6. The system confirms the slot is still free and acquires a database-level lock on the slot.
7. The system creates the reservation record, generates a unique reservation token, and releases the lock.
8. The system displays the confirmation and reservation token to the student.

### Alternate Flow A1: Equipment Fails Calibration Check
*Triggered at step 5 of the main scenario, when the selected equipment's calibration has expired.*
1. The system detects that the equipment's calibration status is "overdue."
2. The system rejects the reservation attempt and displays a message explaining that the instrument is unavailable pending recalibration.
3. The system suggests alternative calibrated instruments of the same type, if any are available.
4. The student may select a different instrument (return to step 2 of the main scenario) or exit the flow.
5. Use case ends without a reservation being created.

### Alternate Flow A2: Slot Taken During Confirmation (Race Condition)
*Triggered at step 6, when two students attempt to lock the same slot concurrently.*
1. The system's locking mechanism detects that the slot was claimed by another request microseconds earlier.
2. The system rejects the second request with a "slot no longer available" message.
3. The system refreshes the availability view so the student can pick another slot.
4. Use case resumes at step 4 of the main scenario.

### Special Requirements
- Response time for the availability check and lock acquisition must meet NFR-001 (≤200 ms under peak load).
- The reservation token must be unique and non-guessable (used later for check-in/check-out verification).
