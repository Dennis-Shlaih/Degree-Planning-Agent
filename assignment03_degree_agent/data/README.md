# Riverview College degree-planning data (fictional)

These files describe a fictional college. They are not Hunter College or CUNY policy.

The agent plans the **Spring 2027** term. The current term is **Fall 2026**: courses listed as `in_progress` have no grade yet.

| File | Contents |
|---|---|
| `catalog.json` | Courses: title, credits, prerequisites, minimum prerequisite grade, terms usually offered |
| `sections.json` | Spring 2027 sections: days, start and end times, open seats, modality |
| `requirements.json` | General degree rules and the Computer Science major's required courses |
| `students.json` | Eight students: major, completed courses with grades, Fall 2026 courses in progress |

## Rules

Every tool and every expected answer follows these rules.

### Grades

- Grade points: A = 4.0, A- = 3.7, B+ = 3.3, B = 3.0, B- = 2.7, C+ = 2.3, C = 2.0, C- = 1.7, D = 1.0, F = 0.0.
- A passing grade is **D or better**. F earns no credit. W (withdrawn) earns no credit and does not count in the GPA.
- When a course was taken more than once, **only the latest attempt counts**, for credits and for the GPA.

### Prerequisites

- A course's `prerequisites` is a list of **groups**. Every group must be met; inside a group, **any one** course is enough. For example, `[["CSCI 210"], ["STAT 205", "MATH 250"]]` means CSCI 210 **and** either STAT 205 or MATH 250.
- A group is met by a completed course whose latest grade is at least the course's `min_grade`. When `min_grade` is `null`, any passing grade (D or better) meets it.

### Eligibility for Spring 2027

Check these in order; the first one that applies is the answer.

1. **`already_taken`**: the student has passed the course, or is taking it now.
2. **`not_eligible`**: at least one prerequisite group is met neither by a completed course nor by a course in progress.
3. **`pending`**: every group is met, but at least one only by a course still in progress. The student is eligible only if they pass that course.
4. **`eligible`**: every group is met by completed courses.

Eligibility looks only at prerequisites. Whether the course has a Spring 2027 section, or open seats, is a separate question answered by the sections data.

### Schedule conflicts

- Two sections **conflict** when they meet on at least one common day **and** their times overlap: each starts before the other ends.
- Times that only touch do **not** conflict: a section ending at 10:40 and one starting at 10:40 can both be taken.
- Online asynchronous sections have no meeting times and never conflict. Online synchronous sections meet at fixed times and can conflict.

### Degree progress

- **Credits earned**: credits of every course whose latest attempt is a passing grade.
- **GPA**: credit-weighted average of grade points over latest attempts graded A to F, rounded to two decimals.
- A bachelor's degree needs at least **120 credits** and a GPA of at least **2.00**.
- The Computer Science major requires every course in `required` and one course from each `choose_one` group, each passed.

### Temporary outage

Looking up sections for **STAT 205** fails with a timeout the first time in a session; looking again succeeds. This simulates a temporary outage, as in the tutorial.
