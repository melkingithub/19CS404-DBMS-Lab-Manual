# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

## Business Context

FlexiFit Gym wants a database to manage its members, trainers, fitness programs, attendance, and payments.

## Requirements

- Members register with name, membership type, and start date.
- Each member can join multiple programs (Yoga, Zumba, Weight Training).
- Trainers are assigned to programs; a program may have multiple trainers.
- Members may book personal training sessions with trainers.
- Attendance is recorded for each session.
- Payments are tracked for memberships and personal training sessions.

## ER Diagram

<img width="1536" height="1024" alt="CityFitnessClubManagement drawio" src="https://github.com/user-attachments/assets/5d575787-9411-47e6-a9af-cb75ce9ea9e8" />


---

## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| **Member** | **MemberID (PK)**, Name, MembershipType, StartDate | Stores member information. |
| **Program** | **ProgramID (PK)**, ProgramName, Type | Stores fitness programs. |
| **Trainer** | **TrainerID (PK)**, Name, Specialization | Stores trainer details. |
| **SessionBooking** | **BookingID (PK)**, MemberID (FK), TrainerID (FK), BookingDate, Status | Stores personal training bookings. |
| **Session** | **SessionID (PK)**, SessionDate, StartTime, EndTime | Stores training session details. |
| **Attendance** | **AttendanceID (PK)**, SessionID (FK), Status, CheckInTime | Records attendance for sessions. |
| **MembershipPayment** | **PaymentID (PK)**, MemberID (FK), Amount, PaymentType | Tracks membership payments. |
| **SessionPayment** | **PaymentID (PK)**, BookingID (FK), PaymentDate, PaymentType | Tracks payments for personal training sessions. |
| **MemberProgram** | **MemberID (FK)**, **ProgramID (FK)**, JoinDate, Status | Associative entity for member-program relationship. |
| **ProgramTrainer** | **ProgramID (FK)**, **TrainerID (FK)**, AssignedDate, Status | Associative entity for trainer-program relationship. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member → MemberProgram | 1 : M | Total (MemberProgram) | A member can join multiple programs. |
| Program → MemberProgram | 1 : M | Total (MemberProgram) | A program can have multiple members. |
| Program → ProgramTrainer | 1 : M | Total (ProgramTrainer) | A program can have multiple trainers. |
| Trainer → ProgramTrainer | 1 : M | Total (ProgramTrainer) | A trainer may teach multiple programs. |
| Member → SessionBooking | 1 : M | Partial | Members can book multiple personal training sessions. |
| Trainer → SessionBooking | 1 : M | Partial | Trainers can conduct multiple personal sessions. |
| SessionBooking → Session | 1 : M | Total (Session) | One booking may include multiple sessions. |
| Session → Attendance | 1 : M | Total (Attendance) | Attendance is recorded for every session. |
| Member → MembershipPayment | 1 : M | Partial | Members can make multiple membership payments. |
| SessionBooking → SessionPayment | 1 : M | Partial | Payments are recorded for booked personal sessions. |

---

## Assumptions

- Every member has a unique MemberID.
- A member may enroll in multiple fitness programs.
- Personal training sessions are booked with exactly one trainer.
- Attendance is recorded for every completed session.
- Membership and personal training payments are stored separately.

---

# Scenario B: City Library Event & Book Lending System

## Business Context

The Central Library wants to manage book lending, cultural events, room bookings, and overdue fines.

## Requirements

- Members borrow books, with loan and return dates tracked.
- Each book has title, author, and category.
- Library organizes events; members can register.
- Each event has one or more speakers/authors.
- Rooms are booked for events and study.
- Overdue fines apply for late returns.

## ER Diagram

<img width="1536" height="1024" alt="CityLibraryBookLendingSystem drawio" src="https://github.com/user-attachments/assets/e670efa8-5ff7-4a2a-b90e-0f4d7055b3b4" />


---

## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| **Member** | **MemberID (PK)**, Name, Phone | Stores library member details. |
| **Book** | **BookID (PK)**, Title, ISBN, CategoryID (FK) | Stores books available in the library. |
| **Category** | **CategoryID (PK)**, CategoryName, Description | Classifies books into categories. |
| **Loan** | **LoanID (PK)**, MemberID (FK), BookID (FK), LoanDate, DueDate, ReturnDate | Tracks borrowed books. |
| **Fine** | **FineID (PK)**, LoanID (FK), Amount, Status | Records overdue fines. |
| **Event** | **EventID (PK)**, EventName, EventDate | Stores library event details. |
| **Speaker** | **SpeakerID (PK)**, Name, Specialization | Stores event speaker details. |
| **EventRegistration** | **RegID (PK)**, MemberID (FK), EventID (FK), RegDate | Records member registrations for events. |
| **Room** | **RoomID (PK)**, RoomName, Capacity | Stores study/event room details. |
| **RoomBooking** | **BookingID (PK)**, RoomID (FK), BookingDate, Purpose | Tracks room bookings. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member → Loan | 1 : M | Total (Loan) | A member can borrow multiple books. |
| Book → Loan | 1 : M | Partial | A book may be borrowed multiple times over its lifetime. |
| Loan → Fine | 1 : 0..1 | Partial | A fine exists only for overdue loans. |
| Category → Book | 1 : M | Partial | Each category contains multiple books. |
| Event → EventRegistration | 1 : M | Total (EventRegistration) | Members register for events. |
| Member → EventRegistration | 1 : M | Partial | A member can register for multiple events. |
| Event → Speaker | M : N | Partial | Events may have multiple speakers and speakers may participate in multiple events. |
| Room → RoomBooking | 1 : M | Partial | Rooms can be booked multiple times. |

---

## Assumptions

- Each book belongs to one category.
- A fine is generated only when the return date exceeds the due date.
- Members can register for multiple events.
- Rooms may be booked either for events or study purposes.
- A speaker can participate in multiple events.

---

# Scenario C: Restaurant Table Reservation & Ordering

## Business Context

A popular restaurant wants to manage reservations, food ordering, billing, and waiter assignments efficiently.

## Requirements

- Customers can reserve tables or walk in.
- Each reservation includes the date, time, and number of guests.
- Customers place food orders linked to reservations.
- Each order contains multiple dishes.
- Dishes belong to categories such as Starter, Main Course, and Dessert.
- Bills are generated for each reservation, including food and service charges.
- Waiters are assigned to serve reservations.

## ER Diagram

<img width="1536" height="1024" alt="RestaurantTableReservationAndOrderingSystem drawio" src="https://github.com/user-attachments/assets/566db927-5959-4a5a-86b8-edf4914760f8" />


---

## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|----------------------|-------|
| **Customer** | **CustomerID (PK)**, CustomerName, Phone, Email | Stores customer information. |
| **Table** | **TableID (PK)**, TableNumber, Capacity, Status | Represents restaurant tables. |
| **Waiter** | **WaiterID (PK)**, WaiterName, Phone | Stores waiter details. |
| **Reservation** | **ReservationID (PK)**, CustomerID (FK), TableID (FK), WaiterID (FK), ReservationDate, ReservationTime, NumberOfGuests, ReservationType | Represents table reservations or walk-in customers. |
| **FoodOrder** | **OrderID (PK)**, ReservationID (FK), OrderTime | Stores orders placed for a reservation. |
| **OrderItem** | **OrderItemID (PK)**, OrderID (FK), DishID (FK), Quantity, SubTotal | Represents individual dishes in an order. |
| **Dish** | **DishID (PK)**, DishName, Price, CategoryID (FK) | Stores menu items. |
| **DishCategory** | **CategoryID (PK)**, CategoryName | Categorizes dishes (Starter, Main Course, Dessert). |
| **Bill** | **BillID (PK)**, ReservationID (FK), FoodAmount, ServiceCharge, TotalAmount, PaymentStatus | Stores billing information for each reservation. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Customer → Reservation | 1 : M | Total (Reservation), Partial (Customer) | A customer can have multiple reservations. |
| Table → Reservation | 1 : M | Partial | A table can be reserved multiple times on different dates/times. |
| Waiter → Reservation | 1 : M | Partial | One waiter can serve multiple reservations. |
| Reservation → FoodOrder | 1 : M | Total (FoodOrder) | Each food order belongs to one reservation. |
| FoodOrder → OrderItem | 1 : M | Total (OrderItem) | Each order consists of one or more order items. |
| Dish → OrderItem | 1 : M | Partial | A dish can appear in many order items. |
| DishCategory → Dish | 1 : M | Partial | Each dish belongs to one category. |
| Reservation → Bill | 1 : 1 | Total | Every reservation generates exactly one bill. |

---

## Assumptions

- A reservation is associated with exactly one customer, one table, and one waiter.
- Walk-in customers are also recorded as reservations with `ReservationType = Walk-in`.
- A reservation may contain multiple food orders.
- Each food order contains one or more order items.
- Each dish belongs to exactly one category.
- Every reservation generates exactly one bill after service.
- Service charges are included in the final bill.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
