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

**Key Relationships:**
- Movies (1) → Shows (Many)
- Theatres (1) → Shows (Many)
- Shows (1) → Seats (Many)
- Customers (1) → Bookings (Many)
- Shows (1) → Bookings (Many)

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
