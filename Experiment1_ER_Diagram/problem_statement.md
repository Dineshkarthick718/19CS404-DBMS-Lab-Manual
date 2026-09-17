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
<img width="1282" height="811" alt="image" src="https://github.com/user-attachments/assets/8a072a50-1aac-405f-9a40-aa537b030ec9" />


### Entities and Attributes

<img width="872" height="672" alt="image" src="https://github.com/user-attachments/assets/5e7f055a-627c-4708-a370-c7597f0055bd" />


### Relationships and Constraints

<img width="852" height="575" alt="image" src="https://github.com/user-attachments/assets/e4372aee-ba07-4d2d-b3b4-58cda5913f1f" />


### Assumptions

- Each session involves exactly one trainer and one member.
- Programs are predefined (Yoga, Zumba, Weight Training, etc.).
- Payments are only for membership or session bookings.
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
<img width="998" height="805" alt="image" src="https://github.com/user-attachments/assets/dc0e8229-a22d-47ac-9956-7d38301b06d6" />


### Entities and Attributes
<img width="871" height="610" alt="image" src="https://github.com/user-attachments/assets/9cd4ca56-f4a9-45a3-b97b-92db7947f2ff" />


### Relationships and Constraints

<img width="871" height="377" alt="image" src="https://github.com/user-attachments/assets/88d1cc3b-ae84-4f04-adff-948246dbb6c9" />


### Assumptions
- Books can be borrowed multiple times by different Members.
- Each Event happens in one Room at a specific time.
- A Speaker can participate in multiple Events.
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

<img width="1175" height="762" alt="image" src="https://github.com/user-attachments/assets/425f706b-7357-45a0-b414-4169b83fc58e" />

### Entities and Attributes
<img width="855" height="440" alt="image" src="https://github.com/user-attachments/assets/3194dea7-2caa-426e-9d77-b9d8a9f7d676" />


### Relationships and Constraints

<img width="862" height="446" alt="image" src="https://github.com/user-attachments/assets/25d64e8f-257a-4460-b144-2c65be600d5b" />

### Assumptions
- One reservation uses one table and one waiter. 
- Bill is generated automatically after service.
- Customer details stored for every reservation.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
