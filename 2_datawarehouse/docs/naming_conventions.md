# Naming Conventions

This document outlines the naming conventions used for schemas, tables, views, columns, stored procedures, and other database objects in the data warehouse.

## Table of Contents

1. [General Principles](#general-principles)
2. [Object Naming Conventions](#object-naming-conventions)
   - [Bronze Tables](#bronze-tables)
   - [Silver Tables](#silver-tables)
   - [Gold Views](#gold-views)
3. [Column Naming Conventions](#column-naming-conventions)
   - [Surrogate Keys](#surrogate-keys)
   - [Business Keys](#business-keys)
   - [Technical Columns](#technical-columns)
4. [Stored Procedure Naming Conventions](#stored-procedure-naming-conventions)

---

## General Principles

- Use **snake_case** with lowercase letters and underscores (`_`) to separate words.
- Use English for all database object names.
- Choose descriptive and business-friendly names.
- Avoid using SQL reserved keywords as object names.
- Apply consistent naming conventions across all Medallion Architecture layers.

---

## Object Naming Conventions

### Bronze Tables

Bronze tables store raw data exactly as received from the source files without any transformations.

**Naming Pattern**

```text
<entity>
```

**Examples**

- `attendance`
- `homework`
- `performance`
- `students`
- `teacher_parent_communication`

---

### Silver Tables

Silver tables store cleansed, standardized, and validated data while preserving the same business entities as the Bronze layer.

**Naming Pattern**

```text
<entity>
```

**Examples**

- `attendance`
- `homework`
- `performance`
- `students`
- `teacher_parent_communication`

---

### Gold Views

Gold objects expose business-ready analytical datasets following the Star Schema.

Dimension views use the following pattern:

```text
dim_<entity>
```

**Examples**

- `dim_students`
- `dim_subjects`

Fact views use the following pattern:

```text
fact_<entity>
```

**Examples**

- `fact_attendance`
- `fact_homework`
- `fact_performance`
- `fact_teacher_parent_communication`

#### Object Prefix Glossary

| Prefix | Description | Example |
|---------|-------------|---------|
| `dim_` | Dimension view | `dim_students` |
| `fact_` | Fact view | `fact_attendance` |

---

## Column Naming Conventions

### Surrogate Keys

Dimension tables use surrogate keys ending with the suffix `_key`.

**Naming Pattern**

```text
<entity>_key
```

**Examples**

- `student_key`
- `subject_key`

---

### Business Keys

Business keys preserve the original identifiers from the source dataset.

**Examples**

- `Student_ID`

---

### Technical Columns

Technical metadata columns begin with the prefix `dwh_`.

**Naming Pattern**

```text
dwh_<column_name>
```

**Example**

- `dwh_create_date`

---

## Stored Procedure Naming Conventions

Stored procedures responsible for loading each Medallion layer follow the naming pattern:

```text
load_<layer>
```

**Examples**

- `load_bronze`
- `load_silver`
