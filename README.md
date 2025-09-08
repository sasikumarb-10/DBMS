**Submitted by:** Sasi Kumar B  
**Reg. No:** 212223060252 
---

## Unnormalized Table (UNF)

| RegID | StudentName | StudentPhone | Course1 | Instructor1 | Grade1 | Course2 | Instructor2 | Grade2 | Advisor | AdvisorPhone |
|-------|------------|--------------|---------|-------------|--------|---------|-------------|--------|---------|--------------|
| R001  | Alice      | 555-1111     | DBMS    | Dr. Rao     | A      | OS      | Dr. Singh   | B+     | Dr. Khan | 555-2222 |
| R002  | Bob        | 555-3333     | CN      | Dr. Rao     | A-     | DBMS    | Dr. Rao     | A      | Dr. Shah | 555-4444 |

**Anomalies present:**  
- Repeating groups (Course1/Course2, Instructor1/Instructor2, Grade1/Grade2)  
- Partial and transitive dependencies possible  

---

## Step 1: First Normal Form (1NF)

**Rules Applied:**  
- Remove repeating groups  
- Ensure atomic values  

**Table after 1NF: CollegeCourseEnrollment**

| RegID | StudentName | StudentPhone | Course | Instructor | Grade | Advisor | AdvisorPhone |
|-------|------------|--------------|--------|-----------|-------|---------|--------------|
| R001  | Alice      | 555-1111     | DBMS   | Dr. Rao   | A     | Dr. Khan | 555-2222 |
| R001  | Alice      | 555-1111     | OS     | Dr. Singh | B+    | Dr. Khan | 555-2222 |
| R002  | Bob        | 555-3333     | CN     | Dr. Rao   | A-    | Dr. Shah | 555-4444 |
| R002  | Bob        | 555-3333     | DBMS   | Dr. Rao   | A     | Dr. Shah | 555-4444 |

**Primary Key:** (RegID, Course)  
**Functional Dependencies:**  
- RegID → StudentName, StudentPhone, Advisor, AdvisorPhone  
- Course → Instructor  
**Anomalies removed:** Eliminated repeating groups  

---

## Step 2: Second Normal Form (2NF)

**Rules Applied:**  
- Remove partial dependencies  

**Tables after 2NF:**  

**1. Student Table**

| RegID | StudentName | StudentPhone | Advisor | AdvisorPhone |
|-------|------------|--------------|---------|--------------|
| R001  | Alice      | 555-1111     | Dr. Khan | 555-2222 |
| R002  | Bob        | 555-3333     | Dr. Shah | 555-4444 |

**Primary Key:** RegID  

**2. Course Table**

| Course | Instructor |
|--------|-----------|
| DBMS   | Dr. Rao   |
| OS     | Dr. Singh |
| CN     | Dr. Rao   |

**Primary Key:** Course  

**3. Enrollment Table**

| RegID | Course | Grade |
|-------|--------|-------|
| R001  | DBMS   | A     |
| R001  | OS     | B+    |
| R002  | CN     | A-    |
| R002  | DBMS   | A     |

**Primary Key:** (RegID, Course)  

**Anomalies removed:** Partial dependencies eliminated  

---

## Step 3: Third Normal Form (3NF)

**Rules Applied:**  
- Remove transitive dependencies  

**Tables after 3NF:**  

**1. Student Table** (unchanged)  

**2. Advisor Table**

| Advisor | AdvisorPhone |
|---------|--------------|
| Dr. Khan | 555-2222    |
| Dr. Shah | 555-4444    |

**Primary Key:** Advisor  

**3. Student-Advisor Table**

| RegID | Advisor |
|-------|---------|
| R001  | Dr. Khan |
| R002  | Dr. Shah |

**Primary Key:** RegID  

**4. Course Table** (unchanged)  

**5. Enrollment Table** (unchanged)  

**Anomalies removed:** Transitive dependencies removed  

---

## Step 4: Boyce-Codd Normal Form (BCNF)

**Rules Applied:**  
- Ensure every determinant is a candidate key  

**Final BCNF Tables:**  
- Student(RegID, StudentName, StudentPhone)  
- Advisor(Advisor, AdvisorPhone)  
- StudentAdvisor(RegID, Advisor)  
- Course(Course, Instructor)  
- Enrollment(RegID, Course, Grade)  

**All functional dependencies preserved. All anomalies removed.**  

---
