# 🐼 Pandas Learn

A repository for learning and practicing data manipulation with the Python pandas library. 

This repo contains my practice notebooks, scripts, and datasets (like IPL match data) as I learn how to analyze and manipulate data using Python.

---

## 🧠 Beginner's Pandas Cheat Sheet

When starting with pandas, some methods sound similar but do very different things. Here is a simple breakdown of the most common confusing concepts!

### 1. `size` vs `count()`

* **`groupby().size()`** *(Rows per group)*
  * **What it does:** It counts the total number of rows in each group.
  * **What it returns:** A single Series. It doesn't care about your columns; it just looks at the group as a whole and tells you how many rows are in it.
  * **Missing values:** *Includes* rows that have `NaN` (missing) values.

* **`groupby().count()`** *(Valid data per column, per group)*
  * **What it does:** It counts the number of non-null (valid) entries for *every single column* within each group.
  * **What it returns:** A DataFrame (unless you specifically select a single column). It gives you a count for every column you grouped.
  * **Missing values:** *Ignores* `NaN` (missing) values.

### 2. `unique()` vs `nunique()`
Imagine you have a basket of fruit: 3 apples, 2 bananas, and 1 orange.
* **`unique()`**: Gives you a list of the *actual names* of the different fruits you have. 
  * *Result:* `['apple', 'banana', 'orange']`
* **`nunique()`**: Gives you the *number* of different types of fruit you have (the "n" stands for number).
  * *Result:* `3`

### 3. `loc` vs `iloc`
These are used to find specific rows or columns in your data.
* **`loc` (Location by Label)**: Looks for things by their **name**. For example, "Find the column named 'Player'".
* **`iloc` (Index Location by Number)**: Looks for things by their **position** (starting at 0). For example, "Find the 3rd column". 

### 4. `head()` vs `tail()`
* **`head(5)`**: Shows you the first 5 rows of your data. Great for getting a quick peek at the top of your dataset.
* **`tail(5)`**: Shows you the last 5 rows of your data. Great for checking the bottom of your dataset.

### 5. `info()` vs `describe()`
* **`info()`**: Gives you the "technical details" of your data. It tells you how many columns you have, if any data is missing, and what type of data is in each column (text, numbers, decimals).
* **`describe()`**: Gives you the "math summary" of your number columns. It automatically calculates the average (mean), minimum, maximum, and totals for you.

# Pandas Grouping and Aggregation Quick Reference

## 1. `groupby().mean()` vs `groupby().transform()`

The easiest way to understand the difference is to think about **what happens to the number of rows** after you run them.

### `groupby().mean()`: The Summarizer
This completely **shrinks** your data. It takes all the rows that belong to a group, calculates the average, and gives you back just **one single row** for that group.
* **Analogy:** Imagine 100 students in 4 classrooms. You ask for a summary report. You get exactly **4 lines** of data—the average score for each classroom. The individual students disappear from view.

### `groupby().transform('mean')`: The Broadcaster
This **keeps your data the exact same size**. It calculates the group average, but instead of shrinking the data, it takes that average and "pastes" it back onto every single original row in that group.
* **Analogy:** You calculate the 4 classroom averages, then hand a sticky note to **every single student** with their classroom's average on it. You still have 100 students, but each has a new piece of information.

**When to use which?**
* Use `.mean()` (or `.agg()`) to build a summary table or dashboard.
* Use `.transform()` to create a new column in your existing dataset (e.g., comparing a single row's value to the group's average).

---

## 2. Finding the Row with the Max Value (using `idxmax`)

When you want to find a maximum value but also need to retrieve other columns from that exact same row (like which bowler bowled the fastest ball), use `.idxmax()` to get the row index.

```python
# 1. Get the indices (row numbers) of the max value for each group
max_indices = df.groupby('batsman')['max_run_in_ball'].idxmax()

# 2. Use those indices to filter your original DataFrame
result = df.loc[max_indices, ['batsman', 'max_run_in_ball', 'bowler', 'match_id']]
```


## 📂 What's in this Repository?

* **`data/`**: Folder containing raw datasets for practice.
* **`matches.csv`**: The IPL matches dataset I am currently analyzing.
* **`ipl.ipynb`**: A Jupyter Notebook where I test out basic pandas functions, filtering, and data exploration.
* **`ipl_taska.py`**: A Python script containing specific data manipulation tasks and logic.

## 🚀 How to Run
1. Make sure you have Python and Pandas installed (`pip install pandas jupyter`).
2. Clone this repository.
3. Open `ipl.ipynb` using Jupyter Notebook to see the code in action!