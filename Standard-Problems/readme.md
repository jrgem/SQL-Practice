# Standard Level Problems 🟡

## Table of Contents
+ [Task](https://github.com/jrgem/SQL-Practice/tree/main/Standard-Problems#task)
+ [Entity](https://github.com/jrgem/SQL-Practice/tree/main/Standard-Problems#entity-relationship-schema)
+ [Questions](https://github.com/jrgem/SQL-Practice/tree/main/Standard-Problems#questions--solution)


## Task
Use hospital database data to answer standard-level questions about patients, admissions and doctors.                   

## Entity Relationship Schema
<p align="center">
<img width="689" alt="table-entity" src="https://github.com/jrgem/SQL-Practice/assets/145512344/f513a598-f51e-4903-b1fd-a30c5952e124">
</p>

## Questions & Solution
### **1. Show unique birth years from patients and order them by ascending.**
```sql
SELECT DISTINCT YEAR(birth_date) AS birth_year
FROM     patients
GROUP BY birth_year;
```
**Steps:**
- Need to select unique values from `birth_date` column using **DISTINCT**.
- Followed by enclosing `birth_date` with **YEAR** function to only gather years resulting in `birth_years’ **alias**.
- Ordering end results by `birth_years` that automatically orders in an ascending manner.

**Solution:**

|  birth_years  |
|  :---:        |
|  1918          |
|  1923          |
|  1925          |
|  1926          |
|  1927          |
|  1928          |

- Displaying **6** of **93** results.


### **2. Show unique first names from the patients table which only occurs once in the list.**
**For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.**
```sql
SELECT first_name
FROM   patients
GROUP BY first_name
     HAVING COUNT (first_name) = 1;
```

**Steps:**
- **SELECT** desired columns.
- **GROUP BY** results using `first_name` column where names with same values will be grouped together.
- **HAVING** statement is only paired with **GROUP BY** and in this case combined with **COUNT** aggregate function to display patient `first_name` that appear once.

**Solution:**
|  first_name  |
|  :---:       |
| Abby         |
| Adelaide     |
| Adelia       |
| Akira        |
| Albert       |
| Aldo         |

- Displaying **6** of **319** results.
- There are 319 patients with unique first names.


### **3. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.**
```sql
SELECT patient_id, first_name
FROM   patients
WHERE  first_name LIKE ’s____%s’;
```

**Steps:**
- After **SELECTING** specific columns, a **WHERE** clause is needed to filter results.
- Filtering `first_name` to select case insensitive exact string comparisons using **LIKE**.
- The patient's `first_name` must begin and end with 's' using 2 characters. We are left with 4 and further inserted as 4 underscores and **%** to welcome `first_name` matching the filters that may also be longer than 6 characters.

**Solution:**
|  patient_id  |  first_name  |
|  :---:       |  :---:       |
| 496          |  Spiros      |
| 629          |  Spiros      |
| 648          | Stanislaus   |
| 1273         | Stanislaus   |
| 1789         | Seamus       |
| 1926         | Stanislaus   |
| 2258         | Spiros       |

- Displaying **7** of **11** results.


### **4. Show patient_id, first_name, last_name from patients whose diagnosis is 'Dementia'.**
**Primary diagnosis is stored in the admissions table.**
```sql
SELECT patients.patient_id, first_name, last_name
FROM   patients
JOIN   admissions
    ON patients.patient_id = admissions.patient_id
WHERE  diagnosis = 'Dementia';
```

**Steps:**
- **SELECT** specific columns and specify what table to pick `patient_id` from as both `patients` and `admissions` tables contain it.
- We will have to **JOIN** the `admissions` table to `patients` table as it contains separate admission values.
- `patients.patient_id` contains table and column to merge. `patient_id` is the **primary key** of `patients` table and **foregin key** of `admissions` resulting in `admissions.patient_id`.
- Further filtering patients who were diagnosed with 'dementia'.

**Solution:**
|  patient_id  |  first_name  |  last_name  |
|  :---:       |  :---:       |    :---:    |
| 160          |  Miranda     |  Delacour   |
| 178          |  David       |  Bustamonte |
| 207          |  Matt        |  Celine     |
| 613          |  Jaki        |  Granger    |
| 836          |  Montana     |  Vimes      |
| 924          |  Simon       |  Spellman   |
| 1201         |  Irene       |  Murphy     |
| 1264         |  Jillian     |  Vakentine  |

- Displaying **8** of **26** results.
- Only 26 patients were diagnosed with dementia.


### **5. Display every patient's first_name.**
**Order the list by the length of each name and then alphabetically.**
```sql
SELECT first_name
FROM   patients
ORDER BY LEN (first_name), first_name;
```

**Steps:**
- **ORDERING BY** `first_name` first and attaching **LENGTH** function to filter names by their character length first and alphabetically second with `first_name`.

**Solution:**
|  first_name  |
|  :---:       |
| Al           |
| Al           |
| Al           |
| Bo           |
| Abe          |
| Abi          |

- Displaying **6** of **4530** results.


### **6. Show the total amount of male patients and the total amount of female patients in the patients table.**
**Display the two results in the same row.**
```sql
SELECT
      (SELECT COUNT (gender) FROM patients WHERE gender = 'M') AS male_patients,
      (SELECT COUNT (gender) FROM patients WHERE gender = 'F') AS female_patients
```

**Steps:**
- Need to perform sub-queries - queries nested inside a query.
- Sub-queries help us display the **COUNT** aggregate function from `gender` column in `patients` table and `gender` is 'M' in one row. Naming the result column as `male_patients`.
- The process is repeated with resulting `female_patients` column.

**Solution:**
|  male_patients  |  female_patients  |
|      :---:      |       :---:       |
|       2468      |        2062       |

- There are 2468 male and 2062 female patients.


### **7. Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'.**
**Show results ordered ascending by allergies then by first_name then by last_name.**
```sql
SELECT first_name, last_name, allergies
FROM   patients
WHERE  allergies = 'Penicillin'
   OR  allergies = 'Morphine'
ORDER BY allergies ASC, first_name, last_name;
```

**Steps:**
- Filter `allergies` results **WHERE** the patient has 'Penicillin' or 'Morphine'.
- **ORDER** results in specified order - `allergies` ascending first, `first_name` second, and `last_name` third.

**Solution:**
|  first_name  |  last_name  |  allergies  |
|  :---:       |  :---:      |    :---:    |
| Briareos     |  Hayes      |  Morphine   |
| Christine    |  Argyros    |  Morphine   |
| Griselda     |  Hopper     |  Morphine   |
| Henry        |  Huang      |  Morphine   |
| Janice       |  Redfield   |  Morphine   |
| Jesse        |  Garnaccia  |  Morphine   |
| Joel         |  Takata     |  Morphine   |

- Displaying **7** of **1104** results.


### **8. Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.**
```sql
SELECT patient_id, diagnosis
FROM   admissions
GROUP BY patient_id, diagnosis
     HAVING COUNT (diagnosis) > 1;
```

**Steps:**
- **GROUPING** results from `patient_id` and `diagnosis` columns.
- First by `patient_id` where patients could have been admitted more than once.
- Then by 'diagnosis' where a patient could have been admitted more than once with the same diagnosis.
- The **HAVING** clause filters results further to patients having the same `diagnosis` more than once with **COUNT**.

**Solution:**
|  male_patients  |          female_patients            |
|      :---:      |               :---:                 |
|       137       |    Pregnancy                        |
|       320       |    Pneumonia                        |
|       1577      |  Congestive Heart Failure           |
|       2004      |  Left Shoulder Rotator Cuff Repair  |
|       2859      |        Severed Spine At C3          |

- Displaying **5** of **11** results.


### **9. Show the city and the total number of patients in the city. Order from most to least patients and then by city name ascending.**
```sql
SELECT city, COUNT (city) AS total
FROM   patients
GROUP BY city
ORDER BY total DESC, city ASC;
```

**Steps:**
- **SELECTING** `city` column and also performing **COUNT** aggregate expression with same column.
- **GROUPING** by `city` column to filter cities by patient origin.
- Finally **ORDERING** by descending `total` **alias** result column and ascending `city`.

**Solution:**
|  male_patients   |  female_patients  |
|      :---:       |       :---:       |
|      Hamilton    |        1938       |
|      Toronto     |        317        |
|      Burlington  |        276        |
|      Brantford   |        147        |
|      Ancaster    |        117        |

- Displaying **5** of **93** results.


### **10. Show first name, last name and role of every person that is either a patient or doctor. The roles are either "Patient" or "Doctor".**
```sql
SELECT first_name, last_name, ('Patient' AS role)
FROM   patients
UNION ALL
SELECT first_name, last_name, ('Doctor' AS role)
FROM   doctors
```

**Steps:**
- Make use of **UNION ALL** function to combine `patients` and `doctors` tables and columns `first_name` and `last_name` contain similar data type fields.
- **UNION ALL** includes duplicate values whereas **UNION** only includes unique values.
- Create new `row` column for each table clarifying whether the person is a 'patient' or 'doctor'.

**Solution:**
|  first_name  |  last_name   |  role     |
|  :---:       |  :---:       |    :---:  |
| Donald       |  Waterfield  |  Patient  |
| Mickey       |  Baasha      |  Patient  |
| Jiji         |  Sharma      |  Patient  |
| Blair        |  Diaz        |  Patient  |
| Claude       |  Walls       |  Doctor   |
| Joshua       |  Green       |  Doctor   |
| Miriam       |  Tregre      |  Doctor   |
| James        |  Russo       |  Doctor   |

- Displaying **8** of **4557** results.


### **11. Show all allergies ordered by popularity. Remove NULL values from query.**
```sql
SELECT allergies, COUNT (allergies) AS total_patients
FROM   patients
GROUP BY allergies
  HAVING allergies IS NOT NULL
ORDER BY total_patients DESC;
```

**Steps:**
- **SELECT** `allergies` and also perform **COUNT** aggregate expression with the same column. Its results will lie on the new `total_patients` column.
- **GROUP BY** function groups `allergies` and NULL values will be taken into account aswell.
- **HAVING** operator will select grouped `allergies` that are not **NULL**.
- We order patient allergies off popularity (which condition is displayed more) by the new `total_patients` column in a **descending** manner.

**Solution:**
|      allergies   |  total_patients   |
|      :---:       |       :---:       |
|      Penicillin  |        1082       |
|      Codeine     |        305        |
|      Sulfa       |        157        |
|      ASA         |        99         |
|     Sulfa Drugs  |        71         |
|      Peanuts     |        52         |

- Displaying **6** of **62** results.
- Penicillin is the most popular allergy among patients.


### **12. Show all patient's first name, last name, and birth date who were born in the 1970s decade. Sort the listing from the earliest birth_date.**
```sql
SELECT first_name, last_name, birth_date
FROM   patients
WHERE  birth_date BETWEEN '1970-01-01' AND '1979-12-31'
ORDER BY birth_date
```
OR
```sql
WHERE YEAR (birth_date) BETWEEN '1970' AND '1979'
```

**Steps:**
- Key is to filter patient `birth_date` using **WHERE** and pairing it with **BETWEEN** operator to set date frame.
- Can be executed by inputing specific birth dates OR taking **YEAR** from `birth_date` and selecting years.

**Solution:**
|  first_name  |  last_name   |  birth_date  |
|  :---:       |  :---:       |    :---:     |
| Frances      |  Kobayakawa  |  1970-01-02  |
| Sunny        |  Burrell     |  1970-01-07  |
| Penelope     |  Beckett     |  1970-01-14  |
| Deborah      |  Stewart     |  1970-01-14  |
| Agusta       |  Decker      |  1970-01-22  |
| Sookie       |  Bearly      |  1970-02-01  |
| Temple       |  Wylie       |  1970-02-10  |

- Displaying **7** of **623** results.
- There are 623 patients born in the 1970s decade.


### **13. We want to display each patient's full name in a single column. Their last name in all upper letters must appear first, then first name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in descending order. (Example: SMITH,jane)**
```sql
SELECT CONCAT (UPPER (last_name), ',', LOWER (first_name)) AS full_name
FROM patients
ORDER BY first_name DESC;
```

**Steps:**
- In column selection, **CONCAT** function combines `last_name` and `first_name` values into a single string.
- However, we need to transform `last_name` values into all upper case using **UPPER** and `first_name` values into lower case using **LOWER**.
- Both separated by a **comma** / **,** with no space in between.
- **ORDER** final results by `first_name` in **descending** manner. Patients with first names starting with z will be displayed first.

**Solution:**
|  first_name           |
|  :---:                |
| MILLER,zoe            |
| CORBIE,ziva           |
| KOBAYAKAWA,zenigata   |
| OVERSTREET,zenigata   |
| BENNETT,zen           |
| MEPHESTO,zelda        |

- Displaying **6** of **4530** results.


### **14. Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.**
```sql
SELECT province_id, SUM (height) AS total_height
FROM   patients
GROUP BY province_id
  HAVING total_height >= 7000;
```

**Steps:**

**Solution:**
|      province_id   |  total_height     |
|      :---:         |       :---:       |
|      BC            |        7720       |
|      NS            |        9765       |
|      ON            |        678037     |


### **15. Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'.**
```sql
SELECT (MAX (weight) - MIN (weight)) AS weight_difference
FROM   patients
WHERE last_name = 'Maroni';
```

**Steps:**

**Solution:**
|  weight_difference  |
|  :---:              |
| 71                  |


### **16. Show all of the days of the month (1-31) and how many admission_dates occured on that day. Sort by the day with most admissions to least admissions.**
```sql
SELECT
      DAY (admission_date) AS month_day,
      COUNT (admission_date) AS total_admissions
FROM  admissions
GROUP BY month_day
ORDER BY total_admissions DESC;
```

**Steps:**

**Solution:**
|      month_day    |  total_admissions  |
|      :---:        |       :---:        |
|      11           |        184         |
|      4            |        184         |
|      9            |        183         |
|      2            |        180         |
|      12           |        179         |
|      6            |        179         |

- Displaying **6** of **31** days.


### **17. Show all columns for patient_id 542's most recent admission_date.**
```sql
SELECT *
FROM   admissions
WHERE  patient_id = '542'
ORDER BY admission_date DESC
LIMIT 1;
```

OR
```sql
SELECT *
FROM   admissions
GROUP BY patient_id
HAVING   patient_id = '542'
  AND    MAX (admission_date)
```

**Steps:**

**Solution:**
|  patient_id  |  admission_date  | discharge_date  |  diagnosis       |  attending_doctor_id  |
|    :---:     |      :---:       |     :---:       |    :---:         |         :---:         |
|     542      |    2019-04-06    |   2019-04-09    |  Abdominal Pain  |           14          |


### **18. Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:**
**1) patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.**

**2) attending_doctor_id contains a 2 and the length of patient_id is 3 characters.**
```sql
SELECT patient_id, attending_doctor_id, diagnosis
FROM   admissions
WHERE  (patient_id % 2 = 1
         AND attending_doctor_id IN (1, 5, 19))
OR     (attending_doctor_id LIKE '%2%'
         AND LEN (patient_id) = 3);
```

**Steps:**

**Solution:**
|  patient_id  |  attending_doctor_id   |  diagnosis               |
|  :---:       |  :---:                 |    :---:                 |
|    9         |  19                    |  Ruptured Appendicitis   |
|   13         |  1                     |  Renal Failure           |
|   15         |  5                     |  Hiatal Hernia           |
|   31         |  19                    |  Cardiovascular Disease  |
|   51         |  1                     |  Undiagnosed Chest Pain  |
|   100        |  22                    |  Deppression, Dementia   |
|   100        |  21                    |  Repiratory Failure      |

- Displaying **7** of **663** results.


### **19. Show first name, last name, and the total number of admissions attended for each doctor. Every admission has been attended by a doctor.**
```sql
SELECT doctors.first_name, doctors.last_name, COUNT (attending_doctor_id) AS attended_admissions
FROM   admissions
JOIN   doctors
 ON    admissions.attending_doctor_id = doctors.doctor_id
GROUP BY attending_doctor_id;
```

**Steps:**

**Solution:**
|  first_name  |  last_name   |  attended_admissions  |
|  :---:       |  :---:       |    :---:              |
| Claude       |  Walls       |  214                  |
| Joshua       |  Green       |  187                  |
| Miriam       |  Tregre      |  168                  |
| James        |  Russo       |  197                  |
| Scott        |  Hill        |  179                  |
| Tasha        |  Phillips    |  168                  |
| Hazel        |  Patterson   |  206                  |

- Displaying **7** of **27** results.


### **20. For each doctor, display their id, full name, and the first and last admission date they attended.**

