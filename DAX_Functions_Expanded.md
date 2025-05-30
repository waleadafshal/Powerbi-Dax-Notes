
# 📊 DAX Functions with Sample Data Model

This document includes key DAX functions with descriptions, syntax, and examples based on a sample Power BI data model.

---

## 🧩 Sample Data Model

We will use the following three tables in our examples:

### 🔹 `Sales`
| SalesID | ProductID | CustomerID | Quantity | Price | Date       |
|---------|-----------|------------|----------|-------|------------|
| 1       | P1        | C1         | 2        | 100   | 2023-01-10 |
| 2       | P2        | C2         | 1        | 200   | 2023-01-12 |
| 3       | P1        | C1         | 1        | 100   | 2023-02-01 |

### 🔹 `Products`
| ProductID | ProductName |
|-----------|-------------|
| P1        | Laptop      |
| P2        | Tablet      |

### 🔹 `Customers`
| CustomerID | CustomerName |
|------------|--------------|
| C1         | Ali          |
| C2         | Sara         |

---

## 🔁 `ALL()` – Clone or Remove Filters

### 📘 Description:
Removes filters or creates a clone of a table without filters.

### 🔧 Syntax:
```dax
ALL(table or column)
```

### 🧪 Examples:
```dax
SalesClone = ALL(Sales)

TotalSalesAllContext = CALCULATE(SUM(Sales[Price]), ALL(Sales))
```

---

## ➕ `ADDCOLUMNS()` – Add Calculated Columns

### 📘 Description:
Adds new columns to a table using expressions.

### 🔧 Syntax:
```dax
ADDCOLUMNS(table, "NewColumnName", expression)
```

### 🧪 Examples:
```dax
SalesWithTotal = ADDCOLUMNS(
    Sales,
    "TotalAmount", Sales[Quantity] * Sales[Price]
)

ProductWithSales = ADDCOLUMNS(
    Products,
    "TotalSales", CALCULATE(SUM(Sales[Price]), Sales[ProductID] = Products[ProductID])
)
```

---

## 📋 `SUMMARIZE()` – Group By Table

### 📘 Description:
Creates a summary table grouped by specific columns with aggregated data.

### 🔧 Syntax:
```dax
SUMMARIZE(table, groupBy_column1, groupBy_column2, "Name", expression)
```

### 🧪 Examples:
```dax
SummaryByProduct = SUMMARIZE(
    Sales,
    Sales[ProductID],
    "TotalQty", SUM(Sales[Quantity])
)

SummaryByCustomer = SUMMARIZE(
    Sales,
    Sales[CustomerID],
    "TotalSales", SUM(Sales[Price])
)
```

---

## 🧮 `CALCULATE()` – Modify Context

### 📘 Description:
Evaluates an expression in a modified filter context.

### 🔧 Syntax:
```dax
CALCULATE(expression, filter1, filter2, ...)
```

### 🧪 Examples:
```dax
SalesForAli = CALCULATE(
    SUM(Sales[Price]),
    Customers[CustomerName] = "Ali"
)

SalesForP1 = CALCULATE(
    SUM(Sales[Price]),
    Sales[ProductID] = "P1"
)
```

---

## ➗ `DIVIDE()` – Safe Division

### 📘 Description:
Performs division and returns an alternate result when denominator is zero.

### 🔧 Syntax:
```dax
DIVIDE(numerator, denominator, [alternateResult])
```

### 🧪 Examples:
```dax
AveragePrice = DIVIDE(SUM(Sales[Price]), SUM(Sales[Quantity]))

SafeDivision = DIVIDE(100, 0, "Undefined")
```

---

## 📅 `PARALLELPERIOD()` – Time Shift

### 📘 Description:
Returns a table shifted in time by a specific number of intervals.

### 🔧 Syntax:
```dax
PARALLELPERIOD(dates, number_of_intervals, interval_type)
```

### 🧪 Examples:
```dax
PreviousMonthSales = CALCULATE(
    SUM(Sales[Price]),
    PARALLELPERIOD('Date'[Date], -1, MONTH)
)
```

---

## 🧠 `VAR` and `VALUES()` – Temporary Variables and Unique Values

### 📘 Description:
- `VAR` allows temporary variable definitions
- `VALUES()` returns unique values from a column

### 🔧 Syntax:
```dax
VAR name = expression
RETURN result

VALUES(column)
```

### 🧪 Examples:
```dax
VARExample = 
VAR TotalQty = SUM(Sales[Quantity])
RETURN TotalQty * 2

CustomerList = VALUES(Sales[CustomerID])
```

---

## 🔝 `TOPN()` – Top N Records

### 📘 Description:
Returns top N rows of a table based on an expression.

### 🔧 Syntax:
```dax
TOPN(n, table, orderBy_expression, [order])
```

### 🧪 Examples:
```dax
Top2Products = TOPN(2, Sales, Sales[Price], DESC)

TopCustomer = TOPN(1, Sales, Sales[Quantity], DESC)
```
    



# Year-over-Year (YoY) Growth

**Definition:**  
Year-over-Year (YoY) Growth measures the percentage change of a metric (e.g., revenue) compared to the same period in the previous year. It helps to analyze business growth while accounting for seasonality and yearly trends.

---

### Formula

\[
\text{YoY Growth} = \frac{\text{Current Year Value} - \text{Previous Year Value}}{\text{Previous Year Value}} \times 100
\]

---

### Example Calculation

- Current Year Revenue (2024): $120,000  
- Previous Year Revenue (2023): $100,000  

\[
\text{YoY Growth} = \frac{120,000 - 100,000}{100,000} \times 100 = 20\%
\]

---

### DAX Measure for Revenue YoY Growth

```DAX
Revenue YoY = 
DIVIDE(
    [Total Revenue] - [Revenue Previous Year],
    [Revenue Previous Year],
    0
)

---

## 📚 Summary

This markdown file demonstrates DAX usage with real-world-like sample data.  
Continue adding your own examples as you grow in Power BI!

