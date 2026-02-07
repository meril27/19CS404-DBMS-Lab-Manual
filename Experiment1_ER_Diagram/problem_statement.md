# ER Diagram Workshop – Submission Template

## DATE: 07.02.2026

#### REG NO: 212224040189
#### NAME : MERIL GOLDLINA A


## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:

<img width="1140" height="802" alt="image" src="https://github.com/user-attachments/assets/f839fe67-d8fd-48ce-9cc1-21706388697e" />



### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|    Member    |    MemberID, Name, Type                |   Store member details    |
|   Trainer     |        TrainerID, Name, Contact            |  Store trainer details     |
|    Program    |         ProgramID, Name, Cost           |     Programs like Yoga/Zumba  |
|    Session    |     SessionID, Date, MemberID (FK), TrainerID (FK)               |    Tracks attendance   |
|    Payment    |          PaymentID, Amount, MemberID (FK), Date          |     Tracks payments by members  |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|       Member–Program       |   M:N         |      Optional for Member, Mandatory for Program         |     A member can join several programs  |
|  Trainer–Program            |    M:N        |           Optional for Trainer, Mandatory for Program    |   Programs may have multiple trainers    |
|       Session–Member       |        1:N    |        Mandatory for Session, Optional for Member      |    Each session is linked to one member   |
|     Session–Trainer         |      1:N      |        Mandatory for Session, Optional for Trainer       |    Each session has one trainer   |
|Member–Payment|       1:N          |     Mandatory for Payment, Optional for Member   |   Payments are associated with members      |



### Assumptions
- Programs are recurring classes; sessions are specific instances.
- Payments cover both memberships and personal sessions.
- Every session is tied to exactly one member and one trainer.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:

<img width="1137" height="801" alt="image" src="https://github.com/user-attachments/assets/79f4463b-87c3-426b-a1b0-08addffbd310" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|    Member    |         MemberID (PK), Name, Contact           |   Library members    |
|    Book    |          BookID (PK), Title, Author, Category          |    Books in the collection   |
|    Loan    |         LoanID (PK), Date, Fine, MemberID (FK), BookID (FK)           | Tracks borrowed books      |
|    Event    |          EventID (PK), Name, Date, RoomID (FK)          |  Library-hosted events     |
|    Speaker    |          SpeakerID (PK), Name, Contact          |   Event speakers or authors    |
|      Booking |        BookingID (PK), Date, RoomID (FK), MemberID (FK)  |      Tracks room reservations     |
### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|         Member–Loan     |     1:N       |       Mandatory for Loan, Optional for Member        |   A member may borrow multiple books    |
|       Member–Event       |     M:N       |         Mandatory for Registration, Optional      |     Members may register for multiple events  |
|      Event–Speaker        |      M:N      |   Mandatory for EventSpeaker, Optional            |  Events may have multiple speakers     |
|      Event–Room        |     1:1       |        Mandatory for Event, Optional for Room       |   Each event is in one room    |
|          Room–Booking    |      1:N      |      Mandatory for Booking, Optional for Room         |  Rooms can be booked by multiple members     |

### Assumptions
- Book copies are not individually modeled.
- Fines are stored for each loan record. 
- Rooms are used for both events and study reservations.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="1137" height="808" alt="image" src="https://github.com/user-attachments/assets/309767a9-7bd0-4d5a-acc7-b943565d5614" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|    Customer    |     CustomerID, Name, Contact               |   CustomerID, Name, Contact    |
|      Waiter  |            WaiterID, Name, Contact        |    Waiter information   |
|    Table    |           TableID, Number, Capacity         |    Restaurant table details   |
|      Reservation  |          ResID, Date, Time, Guests, CustomerID, TableID          |    Table reservations   |
|     Order   |         OrderID, ResID, Status           |    Orders associated with reservations   |
|    Dish    |          DishID, Name, Category          |    Menu items   |
|    Bill    |          BillID, ResID, Amounts          |   Final bill for reservation    |
|    Assignment    |             AssignID, WaiterID, ResID       |   Waiter-reservation assignment    |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|       Customer–Reservation       |   1:N         |     Mandatory for Reservation, Optional for Customer          |     One customer can have multiple reservations  |
|      Reservation–Table        |    1:1        |     Mandatory for Reservation, Optional for Table          |   Each reservation is assigned a table    |
|        Order–Dish      |     M:N       |         Mandatory for Order_Item, Optional for Order/Dish      |    Orders may include multiple dishes   |
|       Reservation–Bill       |      1:1      |        Mandatory for Bill, Optional for Reservation       |  One bill per reservation     |
|      Waiter–Reservation        |      M:N      |       Mandatory for Assignment, Optional for Waiter/Reservation        |    Multiple waiters can serve one reservation   |

### Assumptions
- Split payments are not modeled but could be added as an enhancement.
- Walk-in customers are still recorded.
- Each reservation has a single bill.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
