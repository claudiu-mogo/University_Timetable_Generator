# University_Timetable_Generator

## Task Description

Aim: Make use of 2 algorithms (Hill-Climbing and Monte Carlo Tree Search) to automatically generate a timetable with no conflicts or with the minimum possible number of conflicts. The structure of the timetable should be based on the one of University Politehnica of Bucharest.

The problem involves scheduling activities such as laboratory or seminar sessions, which include the following elements:

- A slot in the timetable occupies 120 minutes (e.g., 8-10), and there are 6 slots in a workday (from 8 to 20) (except for the first test case).
- Classes are held from Monday to Friday (except for the first test case).
- There is a limited number of rooms available for classes. Each room has a maximum capacity of students and is specifically allocated for certain subjects.
- Each subject in the timetable has a specific number of students for which rooms must be allocated.
  
  **Example:**
  - We have a subject X with 90 students and 2 available rooms:
    - Room A with 50 seats available
    - Room B with 20 seats available
  - Valid allocations for subject X include:
    - 2 different intervals in room A (2 * 50 = 100 ≥ 90)
    - 1 interval in room A and 2 intervals in room B (1 * 50 + 2 * 20 = 90 ≥ 90)

- There is a limited number of teachers, each specialized in certain subjects. Each teacher has their own preferences regarding the scheduling of their classes.
- Different teachers can teach the same subject in different rooms during the same time interval.

## Constraints to Consider

To generate a valid timetable, there are two types of constraints: implicit (hard) constraints and violable (soft) constraints.

### 1.1 Implicit / Hard Constraints
Hard constraints are physical or logistical, and once violated, they result in infeasible timetables:

- Only one subject can be taught by one teacher in a room during a given time slot.
- A teacher can teach only one subject in one room during a given time slot.
- A teacher can teach for a maximum of 7 intervals per week.
- A room allows the presence of a number of students less than or equal to its specified maximum capacity during a given time slot.
- All students for a subject must be allocated to classes for that subject. Specifically, the sum of the capacities of the rooms over all intervals in which classes for the subject are held must be greater than or equal to the number of students in that subject. (see Example above)
- All teachers only teach subjects they are specialized in.
- Classes are held in rooms only for the subjects allocated to that room.

### 1.2 Violable / Soft Constraints
Soft constraints relate to the preferences of the teachers. It is preferable to violate soft constraints if it leads to a valid timetable, rather than failing to complete the timetable.

Teacher preferences can be of the following types:

- Preference for certain days or dislike for teaching on a specific day.
  
  **Example:**
  - Monday → the teacher prefers to teach on Monday
  - !Tuesday → the teacher prefers not to teach on Tuesday

- Preference or dislike for certain time intervals on any day.

  **Example:**
  - 8-12 → the teacher prefers to teach in any of the intervals 8-10 or 10-12
  - !14-20 → the teacher prefers not to teach in the intervals 14-16, 16-18, 18-20

- [Bonus] Preference not to have gaps in the timetable longer than X hours.

  **Example:**
  - !Break > 0 → the teacher does not want any break in their timetable
  - !Break > 2 → the teacher does not want gaps longer than 2 hours
