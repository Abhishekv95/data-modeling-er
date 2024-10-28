Tables Design:
Dimension Tables (SCD Type 2 applied):
Dim_Employee

Tracks employee information, with historical versions for each employee.
Includes fields for start and end dates, to handle SCD Type 2 logic.
Dim_Time

Captures the time details like the check-in and check-out times, as well as different time granularity (hour, minute).
Fact Table:
Fact_Employee_Attendance
Stores the check-in and check-out times of employees on a given day, linking to the dimension tables.
Detailed Data Model:
1. Dim_Employee:
This table will capture employee details using SCD Type 2 to keep track of historical data.

Columns:

employee_sk (Surrogate Key) – Primary key, unique for each employee record version.
employee_id (Natural Key) – Unique employee identifier, remains the same across versions.
employee_name – Employee’s name.
department – Employee's department.
is_current – Flag to indicate whether the record is the most recent version (1 for active).
effective_start_date – Start date for the version.
effective_end_date – End date for the version (null for active records).
version_number – Tracks the version of the employee record.
Example Data:

employee_sk	employee_id	employee_name	department	is_current	effective_start_date	effective_end_date	version_number
1	101	John Doe	Sales	1	2023-01-01	NULL	1
2	101	John Doe	Marketing	0	2022-01-01	2022-12-31	2
2. Dim_Time:
This table stores time-related data for the check-in and check-out times.

Columns:

time_id – Surrogate key for time.
hour – Hour of the check-in or check-out.
minute – Minute of the check-in or check-out.
time_of_day – Time description (e.g., ‘morning’, ‘afternoon’, etc.).
Example Data:

time_id	hour	minute	time_of_day
1	09	15	Morning
2	18	45	Evening
3. Fact_Employee_Attendance:
The fact table links the employee’s check-in and check-out times to the dimension tables.

Columns:

attendance_sk – Surrogate key for each attendance record.
employee_sk – Foreign key to Dim_Employee (SCD Type 2).
checkin_time_id – Foreign key to Dim_Time for check-in.
checkout_time_id – Foreign key to Dim_Time for check-out.
attendance_date – Date of check-in and check-out.
hours_worked – Total hours worked for the day.
Example Data:

attendance_sk	employee_sk	checkin_time_id	checkout_time_id	attendance_date	hours_worked
1	1	1	2	2023-10-15	9.5
2	1	1	2	2023-10-16	8.0






Employee Check-In/Check-Out System. This system is designed to track employee attendance, including check-in and check-out times, as well as any shifts, locations, and attendance reports.

Main Entities and Relationships
Employee

Attributes: employee_id (PK), name, department, position, email, phone_number, status
Relationships:
Can have multiple CheckIns and CheckOuts
Assigned to one or more Shifts
Shift

Attributes: shift_id (PK), shift_name, start_time, end_time, shift_type (e.g., morning, evening), location_id (FK)
Relationships:
Linked to multiple Employees
Associated with a Location
Location

Attributes: location_id (PK), location_name, address, city, state, country
Relationships:
Has multiple Shifts
Tracks employee CheckIns and CheckOuts
CheckIn

Attributes: checkin_id (PK), employee_id (FK), shift_id (FK), location_id (FK), checkin_time, date
Relationships:
Linked to an Employee, Shift, and Location
Paired with a corresponding CheckOut for the same employee and shift
CheckOut

Attributes: checkout_id (PK), employee_id (FK), shift_id (FK), location_id (FK), checkout_time, date
Relationships:
Linked to an Employee, Shift, and Location
Associated with a corresponding CheckIn for tracking complete attendance time
AttendanceReport

Attributes: report_id (PK), employee_id (FK), date, checkin_time, checkout_time, shift_id (FK), location_id (FK), hours_worked, status (e.g., Present, Absent, Late)
Relationships:
Aggregates data from CheckIns and CheckOuts
Belongs to an Employee
ER Diagram Design Notes
Employee: Represents an employee in the organization. Each employee is associated with multiple check-ins and check-outs.
Shift: Defines specific shifts, associating employees to particular time slots and locations.
Location: Represents physical locations where employees check in and out. It’s linked to specific shifts and can be used to manage location-based attendance.
CheckIn and CheckOut: Capture the check-in and check-out times for each employee. These records are associated with a specific shift and location.
AttendanceReport: Summarizes daily attendance data, providing a complete record of check-in/out times, total hours worked, and attendance status (e.g., late or present).
