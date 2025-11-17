
# 📘 DAX Formulas Used in the Hospital Emergency Room Dashboard

This file contains **all DAX measures and calculated columns** used in the Power BI project (including the Date Table formulas displayed in your screenshots).  
Copy these into Power BI Desktop or include this file in your GitHub repo.

---

## ✅ 1. No of Patients
```DAX
No of Patients =
DISTINCTCOUNT('Hospital ER Data'[Patient Id])
```

---

## ✅ 2. No of Patients Referred
```DAX
No of Patients Referred =
CALCULATE(
    COUNTROWS('Hospital ER Data'),
    'Hospital ER Data'[Department Referral] <> "None"
)
```

---

## ✅ 3. Avg Wait Time
```DAX
Avg Wait Time =
FORMAT(
    AVERAGE('Hospital ER Data'[patient Waittime]),
    "0.0" & " Min"
)
```

---

## ✅ 4. Satisfaction Score
```DAX
Satisfaction Score =
AVERAGE('Hospital ER Data'[Patient Satisfaction Score])
```

---

## ✅ 5. Waittime Interval
```DAX
Waittime Interval =
SWITCH(
    TRUE(),
    'Hospital ER Data'[Admission Hour] < 2 , "00-02",
    'Hospital ER Data'[Admission Hour] < 4 , "02-04",
    'Hospital ER Data'[Admission Hour] < 6 , "04-06",
    'Hospital ER Data'[Admission Hour] < 8 , "06-08",
    'Hospital ER Data'[Admission Hour] < 10 , "08-10",
    'Hospital ER Data'[Admission Hour] < 12 , "10-12",
    'Hospital ER Data'[Admission Hour] < 14 , "12-14",
    'Hospital ER Data'[Admission Hour] < 16 , "14-16",
    'Hospital ER Data'[Admission Hour] < 18 , "16-18",
    'Hospital ER Data'[Admission Hour] < 20 , "18-20",
    'Hospital ER Data'[Admission Hour] < 22 , "20-22",
    'Hospital ER Data'[Admission Hour] < 24 , "22-24",
    "Above 24"
)
```

---

## ✅ 6. Waittime Status
```DAX
Waittime Status =
IF(
    'Hospital ER Data'[patient Waittime] <= 30,
    "Within Target",
    "Target Missed"
)
```

---

## ✅ 7. Patient Admin Date (Formatted)
```DAX
Patient Admin Date =
FORMAT(
    'Hospital ER Data'[Patient Admission Date],
    "D DDD MMMM, YYYY"
)
```

---

## ✅ 8. Age Group
```DAX
Age Group =
SWITCH(
    TRUE(),
    'Hospital ER Data'[Patient Age] < 10 , "0-09",
    'Hospital ER Data'[Patient Age] < 20 , "10-19",
    'Hospital ER Data'[Patient Age] < 30 , "20-29",
    'Hospital ER Data'[Patient Age] < 40 , "30-39",
    'Hospital ER Data'[Patient Age] < 50 , "40-49",
    'Hospital ER Data'[Patient Age] < 60 , "50-59",
    'Hospital ER Data'[Patient Age] < 70 , "60-69",
    'Hospital ER Data'[Patient Age] < 80 , "70-79",
    'Hospital ER Data'[Patient Age] < 90 , "80-89",
    "90+"
)
```

---

## ✅ 9. Admission Status
```DAX
Admission Status =
IF(
    'Hospital ER Data'[patient Admission Flag] = TRUE(),
    "Admitted",
    "Not Admitted"
)
```

---

## ✅ 10. Admission Hour
```DAX
Admission Hour =
HOUR('Hospital ER Data'[Patient Admission Date])
```

---

## ✅ 11. Date (Date Table column)
> Confirmed from screenshots
```DAX
Date = 'Date Table'[Date]
```

---

## ✅ 12. Date Base (Date Table - Calendar)
```DAX
Date Base =
CALENDAR(
    MIN('Hospital ER Data'[Patient Admission Date]),
    MAX('Hospital ER Data'[Patient Admission Date])
)
```

---

## ✅ 13. Month & Year
```DAX
Month & Year =
'Date Table'[Month Name] & " " & YEAR('Date Table'[Date])
```

---

## ✅ 14. Month Name
```DAX
Month Name =
FORMAT('Date Table'[Date], "MMMM")
```

---

## ✅ 15. Month Number
```DAX
Month Number =
MONTH('Date Table'[Date])
```

---

## ✅ 16. Week Day
```DAX
Week Day =
WEEKDAY('Date Table'[Date], 2)
```

---

# Notes & Tips

- If your model uses a separate Date dimension table, ensure that `Date Base` is created in that Date table, and then mark it as a Date table in Power BI (Modeling -> Mark as Date Table).
- Use `Month Number` to sort `Month Name` by month order in visuals (select Month Name column -> Sort by Column -> Month Number).
- Adjust formatting strings if your locale requires different formats (e.g., `"dd-mm-yyyy"`).
- Double-check column/table names in your model — they must match exactly in DAX.

---

# End of file
