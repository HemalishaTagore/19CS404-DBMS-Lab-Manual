# ER Diagram Workshop – Submission Template

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

<img width="812" height="412" alt="City Fitness Club Management" src="https://github.com/user-attachments/assets/8c69c4f0-2a10-48f9-b3df-a08aba317094" />


### Entities and Attributes

<img width="728" height="279" alt="image" src="https://github.com/user-attachments/assets/f429ab5b-ae24-48a8-9ffa-8d5eb4658c88" />


### Relationships and Constraints

<img width="725" height="307" alt="image" src="https://github.com/user-attachments/assets/f07ddf00-6704-42d1-9da6-0137f28efa29" />


### Assumptions

 - Each personal training session involves exactly one member and one trainer.
 - A payment can be for either a membership fee or a session fee, distinguished by the Purpose attribute.
 - Attendance is modeled as a weak entity dependent on SESSION (one attendance record per session).
 - Group classes (Yoga/Zumba) are represented as PROGRAM enrollments; SESSION is used specifically for
personal training
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

<img width="829" height="462" alt="City Library Event   Book Lending System drawio" src="https://github.com/user-attachments/assets/7a7db29c-179f-470b-a47a-8bb513c2de4a" />


### Entities and Attributes

<img width="727" height="211" alt="image" src="https://github.com/user-attachments/assets/2ff67fdb-fa4f-4b22-b60c-d1184256c989" />


### Relationships and Constraints

<img width="723" height="213" alt="image" src="https://github.com/user-attachments/assets/222cac06-a609-4056-a958-7fb0ebd71152" />


### Assumptions
- Fine_Amount is a derived attribute, calculated from the overdue period after Return_Date.
- A room can be booked either for hosting an event or for individual member study, tracked via RESERVES.
- Each event has at least one speaker/author (total participation from EVENT toward FEATURES).
- A book may be borrowed by many members over time, but only by one member at a time (not modeled explicitly; assumed enforced by application logic / available-copy count).
- Overdue fines apply only when Return_Date exceeds the due date derived from Loan_Date

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
<img width="817" height="482" alt="Restaurant Table Reservation   Ordering drawio" src="https://github.com/user-attachments/assets/ddf317a8-3f91-4652-878b-196bd15e7db0" />



### Entities and Attributes

<img width="723" height="284" alt="image" src="https://github.com/user-attachments/assets/22b4704e-a1fb-48ca-b9ea-acd88e88cbda" />


### Relationships and Constraints
<img width="722" height="288" alt="image" src="https://github.com/user-attachments/assets/7b09d0af-711c-4aa6-8ed6-9ac9983a31ab" />



### Assumptions
- Walk-in customers are modeled as reservations created at the time of arrival (Res_Date/Time = current).
- Total_Amount on BILL is a derived attribute = Food_Charge + Service_Charge.
- Each reservation is assigned exactly one table and one waiter for simplicity (no table/waiter sharing modeled).
- Dish Category (starter/main/dessert) is stored as an attribute of DISH rather than a separate entity, since categories have no additional attributes of their own.
- A reservation may generate multiple orders (e.g., additional rounds) but only one final bill

---
