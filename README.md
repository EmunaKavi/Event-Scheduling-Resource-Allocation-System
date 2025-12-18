## Dashboard
![Dashboard](Dashboard.png)

## Feature Previews
| **Resource Management** | **Event Management** |
|:---:|:---:|
| ![Resource Management](Resource%20Management.png) | ![Event Management](Event%20Management.png) |

A full-stack web application for scheduling events and allocating shared resources (rooms, equipment, instructors) with built-in conflict detection and reporting.

## Features
- **Resources**: Manage rooms, instructors, and equipment.
- **Events**: Schedule workshops, seminars, and classes.
- **Conflict Detection**: Automatically prevents double-booking resources.
- **Reports**: View resource utilization with interactive visualizations.
    - **Utilization Rings**: Percentage-based visual indicators.
    - **Comparison Analysis**: Bar charts comparing bookings vs total hours.

## Tech Stack
- **Backend**: Flask (Python), SQLAlchemy
- **Frontend**: HTML5, Bootstrap 5, Vanilla JS, **Chart.js**
- **Database**: MySQL

## Prerequisites
- Python 3.8+
- MySQL Server

## Setup Instructions

### 1. Database Setup
Create an empty MySQL database:
```sql
CREATE DATABASE event_scheduling_db;
```
Update `.env` with your credentials:
```ini
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=event_scheduling_db
```

### 2. Application Setup
```bash
# Install dependencies
pip install -r requirements.txt

# Run the application
python app.py
```
*Note: The database tables will be created automatically on first run via the `/api/init-db` logic or manual call.*

**First Time Run:**
Use Postman or Curl to initialize tables unique constraints if not auto-created:
`POST http://localhost:5000/api/init-db`

Access the app at `http://localhost:5000`.

## Conflict Logic
The system uses the following logic to detect overlaps:
```python
Existing.start_time < New.end_time AND Existing.end_time > New.start_time
```
This ensures that no two events using the same resource can overlap in time.

## Contact
Submitted by: [Emuna D]

## Test Cases Covered

### A. Event Management
- [x] TC-E01: Create Event (Valid)
- [x] TC-E02: Missing Description (Validating Error)
- [x] TC-E03: Space-only Description (Validating Error)
- [x] TC-E04: Invalid Time Range (Start >= End)

### B. Resource Management
- [x] TC-R01: Create Resource (Valid)
- [x] TC-R04: Duplicate Resource Name (Uniqueness Check)

### C. Resource Allocation
- [x] TC-A01: Allocate Resource (Valid)
- [x] TC-A02: Overlapping Allocation (Conflict Detection)
- [x] TC-A07: Duplicate Allocation (Integrity Check)

### E. Reports
- [x] TC-U01: Utilization Report Generation
