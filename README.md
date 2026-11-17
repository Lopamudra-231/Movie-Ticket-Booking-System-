# 🎬 Movie Ticket Booking System

A MySQL-based Capstone Project that solves the real-life problem of **double booking** in movie theatres using Triggers, Transactions, Views and Audit Logs.

> One seat can be booked only once for one show. If someone tries to book it again, the system automatically blocks it.

### ✨ Features
- ✅ Prevents Double Booking using BEFORE INSERT Trigger
- ✅ Auto-frees seat on Cancel using AFTER UPDATE Trigger
- ✅ Auto-calculates ticket price from Shows table
- ✅ Price change history saved in `price_audit` table
- ✅ Booking history saved in `booking_log` table
- ✅ Transaction + Savepoint for booking multiple seats together
- ✅ 3 Views for Reports - Booking Summary, Seats Left, Movie Collection

### 🛠️ Tech Stack
- **Database:** MySQL 8.0
- **Tool:** MySQL Workbench
- **Design:** Draw.io / ER Diagram
- **Language:** SQL

### 🗂️ Database Design
**8 Tables:**
`movies`, `theatres`, `shows`, `seats`, `customers`, `bookings`, `booking_log`, `price_audit`

**ER Diagram:**
![ER Diagram](docs/ER_Diagram.png)

Movies: movie_id (PK), title, genre, duration, rating
Theatres: theatre_id (PK), theatre_name, city
Shows: show_id (PK), movie_id (FK), theatre_id (FK), show_time, ticket_price
Seats: seat_id (PK), show_id (FK), seat_no, seat_type, is_booked
Customers: customer_id (PK), full_name, phone, email
Bookings: booking_id (PK), customer_id (FK), show_id (FK), seat_id (FK), amount, status

[MOVIES] 1 -----< [SHOWS] >----- 1 [THEATRES]
              |
              | 1
              |
              v Many
            [SEATS]
              |
              | 1
              |
[ CUSTOMERS ] 1 -----< [BOOKINGS]

**Key Relationships:**
MOVIES (1) → SHOWS (Many)
THEATRES (1) → SHOWS (Many)
SHOWS (1) → SEATS (Many)
CUSTOMERS (1) → BOOKINGS (Many)
SHOWS (1) → BOOKINGS (Many)
BOOKINGS (1) → BOOKING_LOG (Many)
SHOWS (1) → PRICE_AUDIT (Many)

### 🚀 How To Run
1. Open MySQL Workbench
2. Run `sql/01_create_tables.sql`
3. Run `sql/02_insert_data.sql`
4. Run `sql/03_triggers.sql`
5. Run `sql/04_views.sql`
6. Test Booking:
```sql
-- Success
INSERT INTO bookings (customer_id, show_id, seat_id) VALUES (1, 1, 1);

-- This will FAIL - Seat already booked!
INSERT INTO bookings (customer_id, show_id, seat_id) VALUES (2, 1, 1);

📁 Project Structure
movie-ticket-booking-system/
├── README.md
├── sql/
│   ├── 01_create_tables.sql
│   ├── 02_insert_data.sql
│   ├── 03_triggers.sql
│   ├── 04_views.sql
│   └── 05_transactions.sql
├── docs/
│   ├── ER_Diagram.png
│   └── Capstone_Report.pdf
└── screenshots/
    ├── booking_success.png
    ├── double_booking_error.png
    └── seats_left_view.png

🎯 What I Learned
Triggers, Stored Procedures, Transactions, Views
Foreign Key Constraints, Normalization
Real-life Database Design

🔮 Future Scope
Online Payment Integration
Frontend with Seat Selection UI
Mobile App
