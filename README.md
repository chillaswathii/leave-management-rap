# Employee Leave Management System (SAP ABAP Cloud, RAP)

A managed RAP business object for leave requests, built with ABAP Cloud on SAP BTP.

## What it does
- Employees create leave requests; the system sets the status and calculates the days.
- Validations block bad data: invalid dates, overlapping leaves, and requests above the leave quota.
- Managers approve or reject requests through custom actions.

## Architecture
Database tables, then CDS interface view, then managed behavior definition, then projection view and projection behavior, then metadata extension (UI annotations), then service definition and OData V4 UI service binding.

## Features
| Feature | Type | Description |
|---|---|---|
| Initial status | Determination | Sets status to S (Submitted) on create |
| Leave days | Determination | Calculates days from start and end date |
| Date check | Validation | End date cannot be before start date |
| Overlap check | Validation | No overlapping requests for the same employee |
| Balance check | Validation | Approved days plus the request cannot exceed quota |
| Approve / Reject | Actions | Change status only from S to A or R |
| Status text and colors | CDS | Shows Submitted, Approved or Rejected with criticality |

## Project structure
- `tables/` database tables
- `cds/` interface and projection views
- `behavior/` behavior definitions and the implementation class
- `ui/` UI annotations (metadata extension)
- `service/` service definition
- `tests/` console classes used to test the logic
- `screenshots/` proof of each test

## Testing
Logic was tested with ABAP console classes using EML (Entity Manipulation Language). Screenshots of each test are in the `screenshots` folder.

## Known limitations
- Leave days include weekends and public holidays.
- The overlap check reads only saved data.
- The Fiori preview could not be run on the training system because of a UCON restriction.

## Tech stack
ABAP Cloud, RAP, CDS, EML, OData V4, Fiori Elements annotations

## Author
chilla swathi