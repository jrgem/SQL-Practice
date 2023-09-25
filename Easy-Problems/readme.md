# Simple Problems 🟢

## Table of Contents
+ [Task](https://github.com/jrgem/SQL-Practice/tree/main/Easy-Problems#table-of-contents/)
+ [Entity Relationship Schema](https://github.com/jrgem/SQL-Practice/tree/main/Easy-Problems#table-of-contents/)

## Task
Use hospital database data to answer easy-level questions about patients, admissions and doctors.

## Entity Relationship Schema
<p align="center">
<img width="689" alt="table-entity" src="https://github.com/jrgem/SQL-Practice/assets/145512344/4ff39843-b2f1-479d-8169-fe0e65334831">
</p>

## Questions and Solutions

**1. Show first name, last name, and gender of patients whose gender is 'M'.**
```sql
SELECT first_name, last_name, gender
FROM   patients
WHERE  gender = 'M';
```

**Steps:**

**Solution:**
