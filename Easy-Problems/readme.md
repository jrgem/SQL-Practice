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
- Showing **3** of **2468** results.

- Showing male patients only.


**2. Show first name and last name of patients who do not have allergies.**
```sql
SELECT first_name, last_name
FROM   patients
WHERE  allergies IS NULL;
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
- Showing **3** of **2059** results.

- Showing patients with no allergies.

**3. Show first name of patients that start with the letter 'C'.**
```sql
SELECT first_name
FROM   patients
WHERE  first_name LIKE 'C%';
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
- Showing **4** of **302** results.

**4. Show first name and last name of patients that weigh within the range of 100 to 200 (inclusive).**
```sql
SELECT first_name, last_name
FROM   patients
WHERE  weight BETWEEN 100 AND 120;
```

**Steps:**
- Select name columns.
- Insert **WHERE** clause with condition to select `weight` row values between 100 and 120 pounds.

**Solution:**
| first_name | last_name   |
| :---:   | :---: |
| Jiji | Sharma  |
| Blair | Diaz  |
| Thomas | ONeill   |
- Showing **3** of **952** results.

**5. Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'.**
```sql
UPDATE patients
SET    allergies = 'NKA'
WHERE  allergies IS NULL;
```

**Steps:**
- **UPDATE** clause sets what table to update from.
- Followed by **SET** to replace values values in the `allergies` column to *'NKA'* **WHERE** `allergies` values are **NULL**.

**Solution:**
  ***Rows Modified: 2059***

**6. Show first name and last name concatinated into one column to show their full name.**
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM   patients
```

**Steps:**
- Use **CONCAT** clause to combine two or more strings together.
- Include an empty ` ' ' ` space in between columns to indicate separation between combined names.
- Ending with **AS** command to rename resulting column with an alias. `full_name` in this case.

**Solution:**
| full_name |
| :---:   |
| Charles Waterfield |
| Mickey Baasha |
| Jiji Sharma |
| Blair Diaz |
| Charles Wolfe |
- Showing **5** of **4530** results.

**7. Show first name, last name, and the full province name of each patient.
Example: 'Ontario' instead of 'ON'.**
```sql
SELECT first_name, last_name, province_name
FROM   patients
JOIN   province_names
  ON   patinets.province_id = province_names.province_id;
```

**Steps:**
- Select name columns and specific `province_name` from the `province_names` table we will **JOIN**.
- Peform a **JOIN** using `patients` and `province_names` tables to condense all data into one table.
- The **ON** clause specifies what column to join tables. The columns usually contain the **primary key** and **foreign key** consisting of unique identifiers - `province_id` in this case.
- `patients.province_id` contains the same unique identifiers as `province_names.province_id` where `province_id` identifies provinces as two characters.

**Solution:**
| first_name | last_name   | province_name    |
| :---:   | :---: | :---: |
| Donald | Waterfield   | Ontario   |
| Mickey | Baasha  | Ontario   |
| Jiji | Sharma   | Ontario   |
| Sonny | Beckett   | Nova Scotia   |
- Showing **4** of **4530** results.

- 'ON' `province_id` is 'Ontario'
- 'NS' `province_id` is 'Nova Scotia'

**8. Show how many patients have a birth_date with 2010 as the birth year.**
```sql
SELECT COUNT (birth_year) AS total
FROM   patients
WHERE  YEAR (birth_year) = 2010;
```

**Steps:**
- **COUNT** function adds the amount of rows in the `birth_year` column with a `total` result **alias**.
- **YEAR** function only extracts the year from a specified date and further filter the given year to only 2010.

**Solution:**
| total |
| :---:   |
| 55 |
- 55 patients were born in 2010.
- Showing **1** of **1** results.

**9. Show the first name, last name, and height of the patient with the greatest height.**
```sql
SELECT first_name, last_name, MAX(height) AS tallest_height
FROM   patients;
```

**Steps:**
- **SELECT** name columns while performing a **MAX** aggregate expression for the `height` column to find the tallest patient.

**Solution:**
| first_name | last_name   | tallest_height    |
| :---:   | :---: | :---: |
| Sam | Haruko   | 226   |
- Sam Haruko is the tallest patient at 226cm.
- Showing **1** of **1** results.

**10. Show all columns for patients who have one of the following patient_ids: 1, 45, 534, 879, 1000.**
```sql
SELECT *
FROM   patients
WHERE  patient_id IN (1, 45, 534, 879, 1000);
```

**Steps:**
- **SELECTING** all columns with **'*'**.
- **WHERE** clause placing desired `patient_ids` in a list for outcome.

**Solution:**
| patient_id | first_name |  last_name  |  gender  |   birth_date  | city     | province_id |   allergies  | height | weight|
|    :---:   |    :---:   |   :---:     |  :---:   |   :---:       | :---:    |    :---:    |   :---:      | :---:  | :---: |
|    1       |    Donald  |  Waterfield |  M       |   1963-02-12  | Barrie   |    ON       |   NULL       | 156    | 65    |
|    45      |    Cross   |  Gordon     |  M       |   2009-03-20  | Ancaster |    ON       |   NULL       | 125    | 53    |
|    534     |    Don     |  Zatar      |  M       |   2008-01-11  | Timmins  |    ON       |   NULL       | 136    | 67    |
|    879     |    Orla    |  Shawn      |  F       |   1967-09-24  | Sarnia   |    ON       |   Penicillin | 149    | 65    |
|    1000    |    Rick    |  Williams   |  M       |   1975-04-13  | Hamilton |    ON       |   Penicillin | 176    | 127   |
- Showing **5** of **5** results.

**11. Show the total number of admissions.**
```sql
SELECT COUNT (admission_date) AS total_admissions
FROM   admissions;
```

**Steps:**
- **COUNT** aggregate expression adds number of rows in `admission_date` column from `admissions` table resulting in `total_admissions` column **alias**.

**Solution:**
| total_admissions |
| :---:   |
| 5067 |
- Showing **1** of **1** results.

- There are 5067 total admissions.

**12. Show all the columns from admissions where the patient was admitted and discharged on the same day.**
```sql
SELECT *
FROM   admissions
WHERE  admission_date = discharge_date
```

**Steps:**
- **SELECTING** all columns following **WHERE** clause filtering days where the patient's `admission_date` and `discharge_date` occured in the same day.

**Solution:**
| patient_id |  admission_date  |  discharge_date  |              diagnosis            |  attending_doctor_id  |
|   :---:    |    :---:         |       :---:      |                :---:              |         :---:         |
|   1        |    2018-09-20    |     2018-09-20   |    Innefective Breathing Pattern  |         24            |
|   9        |    2018-12-31    |     2018-12-31   |    Ruptured Appendicitis          |         19            |
|   10       |    2019-02-27    |     2019-02-27   |    Lower Quadrant Pain            |         27            |
|   17       |    2019-03-04    |     2019-03-04   |    Diabetes Mellitus              |         9             |
|   28       |    2019-03-30    |     2019-03-30   |    Cancer of the Stomach          |         26            |
|   31       |    2018-09-26    |     2018-09-26   |    Cardiovascular Disease         |         19            |
- Showing **6** of **481** results.

**13. Show the patient id and the total number of admissions for patient_id 579.**
```sql
SELECT patient_id, COUNT (admission_date) AS admission_amount
FROM   admissions
WHERE  patient_id = '579';
```

**Steps:**
- **SELECT** desired columns and perform **COUNT** aggregate expression with `admission_date` column as `admission_amount` result **alias**.
- Selecting specific '579' `patient_id` with **WHERE** function.

**Solution:**
| patient_id | admission_amount |
| :---:      |      :---:       |
| 579        |        2         |
- Showing **1** of **1** results.

**14. Based on the cities that our patients live in, show unique cities that are in province_id 'NS'.**
```sql
SELECT DISTINCT city
FROM   patients
WHERE  province_id = 'NS';
```

**Steps:**
- **DISTINCT** function selects unique non-repeating values in the  `city` column.
- The **WHERE** function specifies cities further with an 'NS' `province_id`.

**Solution:**
|    city          | 
|   :---:          |
| Port Hawkesbury  |    
| Halifax          |    
| Inverness        |
- Showing **53** of **3** results.

**15. Write a query to find the first_name, last_name and birth date of patients who have height greater than 160 and weight greater than 70.**
```sql
SELECT first_name, last_name, birth_date
FROM   patients
WHERE  height > 160 AND weight > 70;
```

**Steps:**
- **SELECTING** desired columns.
- **WHERE** function declares constraint where `height` should be greater than 160 **AND** `weight` greater than 70.

**Solution:**
| first_name |  last_name   |  birth_date  |
| :---:      |      :---:   |     :---:    |
| Mickey     |     Baasha   |  1981-05-28  |
| Jiji       |     Sharma   |  1957-09-05  |
| Blair      |     Diaz     |  1967-01-07  |
| Thomas     |     ONeill   |  1993-01-31  |
| Sonny      |     Beckett  |  1952-12-11  |
- Showing **5** of **2091** results.

**16. Write a query to find list of patients first_name, last_name, and allergies from Hamilton where allergies are not null.**
```sql
SELECT first_name, last_name, allergies
FROM   patients
WHERE  city = 'Hamilton AND allergies IS NOT NULL;
```

**Steps:**
- **SELECTING** desired columns.
- **WHERE** function declares constraint where `city` is 'Hamilton' **AND** `allergies` does not have a **NULL** using **IS NOT**.

**Solution:**
| first_name | last_name      | allergies    |
| :---:      | :---:          | :---:        |
| Jiji       | Sharma         | Penicillin   |
| Tom        | Halliwell      | Ragweed      |
| Nino       | Andrews        | Peanuts      |
| John       | Farley         | Gluten       |
| Sam        | Threep         | Sulpha       |
- Showing **5** of **1046** results.
