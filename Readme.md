# Sports Booking Database Management System

This project implements a **Sports Booking Database Management System** using MySQL. It includes the creation of a database schema, tables, views, stored procedures, triggers, and functions to manage a sports facility's booking system. The system allows for managing members, rooms, bookings, and payment statuses efficiently.

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Database Schema](#database-schema)
4. [Setup Instructions](#setup-instructions)
5. [Usage](#usage)
6. [Testing](#testing)
7. [File Structure](#file-structure)
8. [Future Enhancements](#future-enhancements)
9. [Author](#author)
10. [License](#license)

---

## Project Overview

The **Sports Booking Database Management System** is designed to:
- Manage members and their payment dues.
- Handle room bookings with constraints to avoid double bookings.
- Provide procedures for adding, updating, and deleting members and bookings.
- Automate processes like payment updates and cancellations using triggers and functions.

---

## Features

### Core Features:
- **Member Management**: Add, update, and delete members.
- **Room Management**: Manage rooms and their pricing.
- **Booking Management**: Create, update, and cancel bookings with payment tracking.
- **Payment Tracking**: Automatically update payment dues for members.
- **Cancellation Rules**: Enforce cancellation policies with penalties.
- **Data Integrity**: Use foreign keys and constraints to maintain data consistency.

### Advanced Features:
- **Stored Procedures**: Automate repetitive tasks like adding members or making bookings.
- **Triggers**: Automatically handle pending terminations when members with dues are deleted.
- **Functions**: Calculate cancellation counts for penalty enforcement.
- **Views**: Simplify querying member bookings with a `member_bookings` view.

---

## Database Schema

### Tables:
1. **`members`**: Stores member details and payment dues.
2. **`pending_terminations`**: Tracks members deleted with unpaid dues.
3. **`rooms`**: Stores room details and pricing.
4. **`bookings`**: Tracks room bookings, payment statuses, and timestamps.

### Views:
- **`member_bookings`**: Combines booking and room details for easy querying.

### Stored Procedures:
- `insert_new_member`: Add a new member.
- `delete_member`: Delete a member.
- `update_member_password`: Update a member's password.
- `update_member_email`: Update a member's email.
- `make_booking`: Create a new booking and update payment dues.
- `update_payment`: Mark a booking as paid and update member dues.
- `view_bookings`: View bookings by ID.
- `search_room`: Search for available rooms by type and time.
- `cancel_booking`: Cancel a booking with penalty enforcement.

### Triggers:
- **`payment_check`**: Before deleting a member, move them to `pending_terminations` if they have unpaid dues.

### Functions:
- **`check_cancellation`**: Count consecutive cancellations for penalty calculation.

---

## Setup Instructions

### Prerequisites:
- MySQL Server installed on your system.
- A MySQL client (e.g., MySQL Workbench, command-line client).

### Steps:
1. Clone or download this repository to your local machine.
2. Open the `sportsDB.sql` file in your MySQL client.
3. Execute the script to:
   - Create the database.
   - Create tables, views, stored procedures, triggers, and functions.
   - Insert sample data into the database.

---

## Usage

### Key Operations:
1. **Add a Member**:
   ```sql
   CALL insert_new_member('new_id', 'password123', 'email@example.com');
   ```
2. **Make a Booking**:
```sql
CALL make_booking('B1', '2025-04-15', '10:00:00', 'member_id');
```
3. **Cancel a Booking:**
```sql
CALL cancel_booking(1, @message);
SELECT @message;
```
4. **Search for Available Rooms:**
```sql
CALL search_room('Tennis Court', '2025-04-20', '15:00:00');
```
5. **Update Payment Status:**
```sql
CALL update_payment(1);
```
6. **View Bookings:**
```sql
CALL view_bookings('member_id');
```
## Testing

### Manual Testing:

#### Setup:
1. Execute the `sportsDB.sql` file to initialize the database.
2. Use the sample data provided to test the system.

#### Test Scenarios:
1. Add a new member and verify the `members` table.
2. Make a booking and check the `bookings` table.
3. Cancel a booking and verify the `payment_status` and `members.payment_due`.
4. Delete a member with unpaid dues and check the `pending_terminations` table.

#### Edge Cases:
1. Attempt to double-book a room at the same time.
2. Cancel a booking on or after the booked date.
3. Delete a member with no dues and verify no entry in `pending_terminations`.

### Automated Testing:
- Use a MySQL testing framework or write scripts to validate stored procedures, triggers, and functions.

---


---

## Future Enhancements

1. **User Authentication**:
   - Add a login system with hashed passwords.
2. **Enhanced Reporting**:
   - Create additional views for financial reports and booking trends.
3. **Penalty Customization**:
   - Allow dynamic configuration of cancellation penalties.
4. **Integration**:
   - Build a front-end application to interact with the database.

---

## Author

This project was developed by **Gowtham Pentela**. For any queries or suggestions, feel free to reach out.

---
