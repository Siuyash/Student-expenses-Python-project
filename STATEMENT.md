suy
::: {align="center"}
# 🔴🟡 Student Expense Tracker ⚫

### Project Statement

**Suyash Dixit**\
VIT Bhopal University · Mechanical Engineering (AI and Robotics)
:::

------------------------------------------------------------------------

## 🔴 1. Problem Statement

Students often have to manage their money carefully while paying for
everyday needs such as food, travel, books, rent, and entertainment.
Small purchases can add up over time, and without a simple way to record
them, it can be difficult to understand where money is going or whether
spending is staying within a monthly budget.

The **Student Expense Tracker** is a simple, terminal-based Python
application designed to help with this problem. It allows users to set a
monthly budget, record expenses, review their spending, and see a
summary of expenses by category. The information is saved locally in a
JSON file so it can be accessed again when the program is run later.

## 🟡 2. Scope of the Project

This project focuses on basic personal expense tracking through a
command-line interface. Its scope includes:

-   Setting and saving a monthly budget in rupees.
-   Recording an expense with a title, category, amount, and date.
-   Organizing expenses into categories: food, travel, books, rent, fun,
    and other.
-   Viewing all recorded expenses.
-   Calculating total spending and showing the amount remaining against
    the budget.
-   Displaying a category-wise spending breakdown with percentages and
    simple text bars.
-   Identifying the largest single expense.
-   Warning the user when total recorded spending exceeds the set
    budget.
-   Deleting an expense from the saved list.
-   Saving and loading data through a local `expenses.json` file.

The project is intentionally limited to a lightweight, local
application. It does not include a graphical interface, online
synchronization, user accounts, or a database server.

## ⚫ 3. Target Users

The main target users are:

-   **College and university students** who want to keep track of
    day-to-day spending.
-   **Students living away from home** who need to monitor expenses such
    as food, rent, and travel.
-   **Beginners learning Python** who want to understand practical uses
    of functions, loops, input validation, lists, dictionaries, and JSON
    file handling.
-   **Anyone looking for a simple local expense log** without needing a
    separate budgeting application.

The project is designed for individual use and does not require advanced
technical knowledge beyond running a Python script in a terminal.

## 🔴 4. High-Level Features

### Budget Management

Users can set a monthly budget in rupees and view how much remains after
recorded spending.

### Expense Recording

Users can enter an expense title, select a category, and provide the
amount. The current date is recorded automatically.

### Expense Categories

Expenses are grouped into food, travel, books, rent, fun, and other.
Unrecognized category names are placed under `other`.

### Expense List

Users can view their saved expenses, including date, category, amount,
and title.

### Spending Summary

The program calculates total spending, summarizes amounts by category,
displays category percentages, and identifies the largest individual
expense.

### Budget Warning

When recorded spending exceeds the set budget, the program displays a
warning showing the amount over budget.

### Delete an Expense

Users can remove an expense by selecting its number from the displayed
list.

### Local Data Storage

The budget and expense records are saved to `expenses.json`, allowing
the information to remain available between program sessions.

------------------------------------------------------------------------

::: {align="center"}
**🔴 Track expenses · 🟡 Understand spending · ⚫ Plan your budget**
:::
