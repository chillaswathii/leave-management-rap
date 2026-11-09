# Employee Leave Management System (SAP ABAP Cloud, RAP)

A draft-enabled, managed RAP business object for leave requests with a Fiori Elements UI, built with ABAP Cloud on SAP BTP.

## What it does
- Employees create leave requests; the system sets the status and calculates the days.
- Validations block bad data: invalid dates, overlapping leaves, and requests above the leave quota.
- Managers approve or reject requests through custom actions.
- Users can save work in progress as a draft before creating the request.

## Architecture
Database tables (with a draft table), then CDS interface view, then managed behavior definition with draft, then projection view and projection behavior, then metadata extension (UI annotations), then service definition and OData V4 UI service binding.

## Features
| Feature | Type | Description |
|---|---|---|
| Initial status | Determination | Sets status to S (Submitted) on create |
| Leave days | Determination | Calculates days from start and end date |
| Date check | Validation | End date cannot be before start date |
| Overlap check | Validation | No overlapping requests for the same employee |
| Balance check | Validation | Approved days plus the request cannot exceed quota |
| Approve / Reject | Actions | Change status only from S to A or R |
| Feature control | Instance features | Approve and Reject are enabled only on saved requests in status S |
| Draft handling | RAP draft | Users save work in progress before creating the request |
| Status text and colors | CDS | Shows Submitted, Approved or Rejected with criticality |

## Project structure
- `tables/` database tables, including the draft table
- `cds/` interface and projection views
- `behaviour/` behaviour definitions and the implementation class
- `ui/` UI annotations (metadata extension)
- `service/` service definition
- `tests/` console classes used to test the logic
- `screenshots/` proof of each test

## Testing
Logic was tested with ABAP console classes using EML (Entity Manipulation Language) and through the Fiori Elements app (create, validations, approve, reject). Screenshots are in the `screenshots` folder.

## Known limitations
- Leave days include weekends and public holidays.
- The overlap check reads only saved data.
- Authorization is global, so any user can approve. Instance authorization is a planned improvement.
- The employee ID is typed by the user and not taken from the logged-in user.
- The app was tested through the ADT preview and is not deployed to a Fiori Launchpad.

## Possible improvements
- Instance authorization so only managers can approve
- Value help for leave types
- Holiday-aware day calculation
- ABAP Unit tests

## Tech stack
ABAP Cloud, RAP (managed, draft), CDS, EML, OData V4, Fiori Elements annotations

## Author
Chilla Swathi
