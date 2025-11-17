
✅ Project: Token Count Analysis on Online Retail Dataset

**Goal:** Calculate the number of tokens (word entries) from the *Description* column and show token counts grouped by **each date**.

---

1. Introduction

This project analyzes a large Online Retail dataset and computes the total number of tokens (words) from the *Description* field. Tokenizing product descriptions helps understand text density, customer purchase behavior, and data quality trends over time.

The main objective is to **calculate the number of tokens and display the total token count per day** for the entire dataset.

---

2. Steps Followed (As per your execution)

Step 1 – Load Dataset

PySpark’s DataFrameReader is used to load the CSV file:

```python
df = spark.read.csv(input_path, header=True, inferSchema=True)
```

---

Step 2 – Data Cleaning

Convert `InvoiceDate` to proper date format:

```python
df = df.withColumn("InvoiceDate", to_date(col("InvoiceDate")))
```

Null descriptions are replaced with empty strings:

```python
df = df.fillna({"Description": ""})
```

---

Step 3 – Tokenize “Description” Column

We split the description into words and count tokens:

```python
df = df.withColumn("Tokens", size(split(col("Description"), " ")))
```

---

Step 4 – Group by Date and Sum Tokens

We compute the total tokens for each date:

```python
result = df.groupBy("InvoiceDate").sum("Tokens")
```

---

Step 5 – Save Output

Output is saved as a CSV file:

```python
result.coalesce(1).write.mode("overwrite").csv(output_path)
```

Output directory:
**D:/token_count_project/output/token_counts.csv**

---

3. Outcome / Result

After successfully running the script, a table like this was generated:

| InvoiceDate | Total Tokens |
| ----------- | ------------ |
| 2011-01-04  | 5447         |
| 2011-01-06  | 8404         |
| 2011-01-05  | 8043         |
| ...         | ...          |

(Your console displayed all values.)

This shows how many words were present across all product descriptions on each date.

---

4. Skills Learned

✔ Data loading using PySpark
✔ Date handling and text preprocessing
✔ Tokenization using `split()` and `size()`
✔ Grouping and aggregation
✔ Writing output back to CSV in Spark
✔ Working with large datasets efficiently

---

5. Conclusion

This project demonstrates how PySpark can be used for large-scale text analysis. Counting tokens from descriptions helps reveal patterns in customer activity, catalog text complexity, and overall dataset quality over time. The approach is scalable, fast, and suitable for real-world analytics workflows.

---

