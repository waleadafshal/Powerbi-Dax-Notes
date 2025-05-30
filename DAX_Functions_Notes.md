# 📊 DAX Functions Notes

A growing list of DAX functions used in Power BI with examples and explanations.

---

## 🔁 `ALL()` – Clone Table

> **Use Case:** When you need a version of a table without any filters.

```dax
Sales_Clone = ALL(Sales)
```

---

## ➕ `ADDCOLUMNS()` – Add Calculated Columns

Adds new columns to a table with custom expressions.

```dax
ADDCOLUMNS(
    Table,
    "NewColumnName1", Expression1,
    "NewColumnName2", Expression2
    -- Add more columns as needed
)
```

---

## 📋 `SUMMARIZE()` – Group By

> Groups a table by specified columns and allows you to apply aggregations.

```dax
SUMMARIZE(
    Sales,
    Sales[Region],
    Sales[Product],
    "Total Sales", SUM(Sales[Amount])
)
```

---

## 🧮 `CALCULATE()` – Modify Context

Changes the filter context of a calculation.

```dax
CALCULATE(
    SUM(Sales[Amount]),
    Sales[Region] = "North"
)
```

---

## ➗ `DIVIDE()` – Safe Division

Avoids divide-by-zero errors.

```dax
DIVIDE(numerator, denominator, [alternateResult])
```

Example:

```dax
DIVIDE(SUM(Sales[Profit]), SUM(Sales[Revenue]), 0)
```

---

## 📅 `PARALLELPERIOD()` – Shift Time Period

Shifts time context by a specified interval.

```dax
PARALLELPERIOD(
    'Date'[Date],
    -1,
    MONTH
)
```

Returns the same period from the previous month.

---

## 🧠 `VAR` – Define Variables for Readability

Improves code clarity and performance.

```dax
SalesGrowth :=
VAR PrevSales = [Sales Last Month]
VAR CurrSales = [Sales This Month]
RETURN
    DIVIDE(CurrSales - PrevSales, PrevSales)
```

---

## 📚 `ADDCOLUMNS()` + `RELATED()` – Add Related Table Info

You can add related data to a table using both:

```dax
ADDCOLUMNS(
    Sales,
    "Quarter", RELATED('Date'[Quarter])
)
```

---

## 🎯 `VALUES()` – Distinct Values in Current Filter Context

```dax
VALUES(ColumnName)
```

Returns a distinct list of values from a column within the current filter context.

---

## 🔝 `TOPN()` – Top N Records

Returns the top N rows from a table based on expression.

```dax
TOPN(
    5,
    Sales,
    Sales[Revenue],
    DESC
)
```

---

## 🚫 `ALL()` – Remove Filters

Used in `CALCULATE()` to ignore current filters.

```dax
CALCULATE(
    SUM(Sales[Amount]),
    ALL(Sales)
)
```

---

Feel free to keep updating this file as you learn more DAX functions!
