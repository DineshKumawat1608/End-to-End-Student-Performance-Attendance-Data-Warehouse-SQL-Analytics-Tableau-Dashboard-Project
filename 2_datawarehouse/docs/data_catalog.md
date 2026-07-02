# Data Catalog for Gold Layer

## Overview

The Gold Layer is the business-level data representation, structured to support analytical and reporting use cases. It consists of **dimension views** and **fact views** organized in a **Star Schema** for student performance and attendance analysis.

---

### 1. **gold.dim_students**

- **Purpose:** Stores student information used across all analytical fact views.

- **Columns:**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| student_key | BIGINT | Surrogate key uniquely identifying each student record in the dimension view. |
| Student_ID | VARCHAR(10) | Business key representing the unique identifier assigned to each student. |
| student_name | VARCHAR(50) | Student's full name after standardization. |
| Date_of_Birth | DATE | Student's date of birth. |
| grade | VARCHAR(20) | Grade level in which the student is enrolled. |
| contact_number | VARCHAR(25) | Standardized emergency contact number for the student. |

---

### 2. **gold.dim_subjects**

- **Purpose:** Stores the unique list of academic subjects used throughout the analytical model.

- **Columns:**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| subject_key | BIGINT | Surrogate key uniquely identifying each subject. |
| subject_name | VARCHAR(50) | Name of the academic subject (e.g., Mathematics, Science, English). |

---

### 3. **gold.fact_attendance**

- **Purpose:** Stores student attendance records for reporting and attendance analysis.

- **Columns:**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| student_key | BIGINT | Surrogate key linking to the student dimension. |
| subject_key | BIGINT | Surrogate key linking to the subject dimension. |
| attendance_date | DATE | Date on which attendance was recorded. |
| Attendance_Status | VARCHAR(50) | Attendance status of the student (e.g., present, absent, late). |

---

### 4. **gold.fact_homework**

- **Purpose:** Stores homework assignments and completion information for analytical reporting.

- **Columns:**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| student_key | BIGINT | Surrogate key linking to the student dimension. |
| subject_key | BIGINT | Surrogate key linking to the subject dimension. |
| assignment_name | VARCHAR(50) | Name of the homework assignment. |
| assignment_due_date | DATE | Due date of the homework assignment. |
| assignment_status | VARCHAR(10) | Current completion status of the homework assignment. |
| grade_feedback | VARCHAR(5) | Grade or evaluation received for the assignment. |
| guardian_signature | VARCHAR(5) | Indicates whether the assignment was signed by the student's guardian. |

---

### 5. **gold.fact_performance**

- **Purpose:** Stores student academic performance metrics for reporting and analysis.

- **Columns:**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| student_key | BIGINT | Surrogate key linking to the student dimension. |
| subject_key | BIGINT | Surrogate key linking to the subject dimension. |
| exam_score | DECIMAL(6,2) | Student's score achieved in the examination. |
| homework_completion_percentage | INT | Percentage of homework completed by the student. |
| teacher_comments | VARCHAR(300) | Teacher's remarks or feedback regarding the student's performance. |

---

### 6. **gold.fact_teacher_parent_communication**

- **Purpose:** Stores communication records exchanged between teachers and parents.

- **Columns:**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| student_key | BIGINT | Surrogate key linking to the student dimension. |
| communication_date | DATE | Date on which the communication took place. |
| message_type | VARCHAR(50) | Category of communication (e.g., Reminder, Feedback, Notice). |
| message_content | VARCHAR(300) | Content of the communication message exchanged between the teacher and parent. |
