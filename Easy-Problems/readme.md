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
- Select specific columns.
- Insert **WHERE** clause with condition to filter the `gender` column to only display male patients using the **=** operator for exact string comparison.

**Solution:**
| first_name | last_name   | gender    |
| :---:   | :---: | :---: |
| Donald | Waterfield   | M   |
| Mickey | Baasha  | M   |
| Jiji | Sharma   | M   |

- Showing male patients only.


**2. Show first name and last name of patients who do not have allergies.**
```sql
SELECT first_name, last_name
FROM patients
WHERE allergies IS NULL;
```

**Steps:**
- Select name columns.
- Inset **WHERE** clause with condition to filter whether patients have/do not have allergies using **IS NULL**.
- The `allergies` column shows the type of allergy a patient has or a **NULL** if no allergy is present.

**Solution:**
| first_name | last_name   |
| :---:   | :---: |
| Donald | Waterfield   |
| Blair | Diaz  |
| Thomas | ONeill   |

- Showing patients with no allergies.

**3. Show first name of patients that start with the letter 'C'.**
```sql
SELECT first_name
FROM patients
WHERE first_name LIKE 'C%';
```

**Steps:**
- Select first name column.
- Insert **WHERE** clause with condition to filter `first_name` starting with 'C' using the **LIKE** case insensitive exact string comparison.
- Followed by **%** as it can be used anywhere in a string to match a sequence of zero or more characters.

**Solution:**
| first_name |
| :---:   |
| Charles |
| Cedric |
| Charles |
| Cross |
