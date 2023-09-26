# Standard Level Problems 🟡

## Table of Contents
+ [Task](https://github.com/jrgem/SQL-Practice/tree/main/Standard-Problems#task)
+ [Entity](https://github.com/jrgem/SQL-Practice/tree/main/Standard-Problems#entity-relationship-schema)

## Task
Use hospital database data to answer standard-level questions about patients, admissions and doctors.                   

## Entity Relationship Schema
<p align="center">
<img width="689" alt="table-entity" src="https://github.com/jrgem/SQL-Practice/assets/145512344/f513a598-f51e-4903-b1fd-a30c5952e124">
</p>

**1. Show unique birth years from patients and order them by ascending.**
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

**2. Show unique first names from the patients table which only occurs once in the list.
For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.**
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

**3. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.**
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

**4. Show patient_id, first_name, last_name from patients whose diagnosis is 'Dementia'.
Primary diagnosis is stored in the admissions table.**

**5. Display every patient's first_name.
Order the list by the length of each name and then alphabetically.**

**6. Show the total amount of male patients and the total amount of female patients in the patients table.
Display the two results in the same row.**

**7. Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'.
Show results ordered ascending by allergies then by first_name then by last_name.**

**8. Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.**

**9. Show the city and the total number of patients in the city. Order from most to least patients and then by city name ascending.**

**10. Show first name, last name and role of every person that is either a patient or doctor. The roles are either "Patient" or "Doctor".**

**11. Show all allergies ordered by popularity. Remove 'NKA' and NULL values from query.**

**12. Show all patient's first name, last name, and birth date who were born in the 1970s decade. Sort the listing from the earliest birth_date.**

**13. We want to display each patient's full name in a single column. Their last name in all upper letters must appear first, then first name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in descending order.**
- EX: SMITH,jane

**14. Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.**

**15. Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'.**

**16. Show all of the days of the month (1-31) and how many admission_dates occured on that day. Sort by the day with most admissions to least admissions.**

**17. Show all columns for patient_id 542's most recent admission_date.**

**18. Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:**
- patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
- attending_doctor_id contains a 2 and the length of patient_id is 3 characters.

**19. Show first name, last name, and the total number of admissions attended for each doctor. Every admission has been attended by a doctor.**

**20. For each doctor, display their id, full name, and the first and last admission date they attended.**

**21. Display the total amount of patients for each province. Order by descending.**

**22. For each admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.**

**23. Display the number of duplicate patients based on their first name and last name.**
- Example: A patient with an identical name can be considered a duplicate.

**24. Display patient's full name, height in the unit feet rounded to 1 decimal, weight in the unit pounds rounded to 0 decimals, birth_date, gender non-abbreviated.**
- Convert CM to feet by dividing by 30.48.
- Conver KG to pounds by multiplying by 2.205.

**25. Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table.** 
- (Their patient_id does not exist in any admissions.patient_id rows.)
