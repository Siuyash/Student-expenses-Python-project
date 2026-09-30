# Student-expenses-Python-project
The Student Expense Tracker is a simple, terminal-based application developed using Python to help students manage their daily expenses and monthly budget. The main objective of this project is to provide an easy and practical way to record spending, monitor expenses, and understand personal financial habits.
Student Expense Tracker:

PYTHON CODE FOR STUDENT EXPENSES TRACKER:


import json
import os
from datetime import date

FILE = "expenses.json"

CATEGORIES = ["food", "travel", "books", "rent", "fun", "other"]


def load_data():
    # if the file isn't there yet (first run) just start empty
    if not os.path.exists(FILE):
        return {"budget": 0, "expenses": []}
    with open(FILE, "r") as f:
        return json.load(f)


def save_data(data):
    with open(FILE, "w") as f:
        json.dump(data, f, indent=2)


def get_number(prompt):
    # keeps asking until the user types an actual number
    while True:
        try:
            value = float(input(prompt))
            if value < 0:
                print("  can't be negative, try again")
                continue
            return value
        except ValueError:
            print("  that's not a number, try again")


def set_budget(data):
    data["budget"] = get_number("Monthly budget (Rs): ")
    save_data(data)
    print("Budget saved!\n")


def add_expense(data):
    title = input("What did you spend on? ").strip()
    if title == "":
        title = "unnamed"

    print("Categories:", ", ".join(CATEGORIES))
    category = input("Category: ").strip().lower()
    if category not in CATEGORIES:
        print("  not in the list, putting it under 'other'")
        category = "other"

    amount = get_number("Amount (Rs): ")

    data["expenses"].append({
        "title": title,
        "category": category,
        "amount": amount,
        "date": str(date.today()),
    })
    save_data(data)
    print("Added.\n")

    # little warning if we crossed the budget
    total = sum(e["amount"] for e in data["expenses"])
    if data["budget"] > 0 and total > data["budget"]:
        print("!! You've gone over your budget by Rs", round(total - data["budget"], 2), "\n")


def show_all(data):
    if not data["expenses"]:
        print("Nothing added yet.\n")
        return

    print("\n#   Date         Category   Amount     Title")
    print("-" * 50)
    for i, e in enumerate(data["expenses"], start=1):
        print(f"{i:<3} {e['date']}   {e['category']:<10} {e['amount']:<10.2f} {e['title']}")
    print()


def summary(data):
    expenses = data["expenses"]
    if not expenses:
        print("No expenses to summarize yet.\n")
        return

    total = sum(e["amount"] for e in expenses)

    # add up each category
    by_cat = {}
    for e in expenses:
        by_cat[e["category"]] = by_cat.get(e["category"], 0) + e["amount"]

    print("\n--- Summary ---")
    print("Total spent:", round(total, 2))

    if data["budget"] > 0:
        left = data["budget"] - total
        print("Budget:", data["budget"])
        print("Left:", round(left, 2))

    print("\nBy category:")
    # biggest spending first
    for cat, amt in sorted(by_cat.items(), key=lambda x: x[1], reverse=True):
        percent = amt / total * 100
        bar = "#" * int(percent / 5)
        print(f"  {cat:<8} {amt:>8.2f}  {percent:>5.1f}%  {bar}")

    biggest = max(expenses, key=lambda e: e["amount"])
    print("\nBiggest single expense:", biggest["title"], "-", biggest["amount"])
    print()


def delete_expense(data):
    show_all(data)
    if not data["expenses"]:
        return
    try:
        num = int(input("Number to delete (0 to cancel): "))
    except ValueError:
        print("Not a valid number.\n")
        return

    if num == 0:
        return
    if 1 <= num <= len(data["expenses"]):
        removed = data["expenses"].pop(num - 1)
        save_data(data)
        print("Deleted:", removed["title"], "\n")
    else:
        print("No expense with that number.\n")


def main():
    data = load_data()
    print("=== Student Expense Tracker ===")

    while True:
        print("1. Set budget")
        print("2. Add expense")
        print("3. View all expenses")
        print("4. Summary")
        print("5. Delete an expense")
        print("6. Quit")
        choice = input("Pick one: ").strip()

        if choice == "1":
            set_budget(data)
        elif choice == "2":
            add_expense(data)
        elif choice == "3":
            show_all(data)
        elif choice == "4":
            summary(data)
        elif choice == "5":
            delete_expense(data)
        elif choice == "6":
            print("Bye, spend wisely!")
            break
        else:[README.md](https://github.com/user-attachments/files/32865065/README.md)

            print("Didn't get that, try again.\n")


if __name__ == "__main__":
    main()
    ::: {align="center"}

README file Main points:
213ojfg
#Student Expense Tracker 

### A simple Python project to keep track of student spending

**Created by Suyash Dixit**\
VIT Bhopal University · Mechanical Engineering (AI and Robotics)

![Python](https://img.shields.io/badge/Python-3.x-yellow?style=for-the-badge&logo=python&logoColor=black)
![Project](https://img.shields.io/badge/Project-Student%20Expense%20Tracker-red?style=for-the-badge)
![Storage](https://img.shields.io/badge/Data-JSON-black?style=for-the-badge)
:::

------------------------------------------------------------------------

## 🟡 About the Project

Managing money as a student can be a little difficult, especially when
small daily expenses start adding up. I made this **Student Expense
Tracker** as a simple way to record expenses, set a monthly budget, and
understand where the money is going.

The program runs in the terminal, so there is no complicated interface
to learn. It stores the information in a JSON file, which means your
saved expenses are still available the next time you run the program.

## 🔴 Features

-   **Set a monthly budget** in rupees.
-   **Add expenses** with a title, category, amount, and date.
-   **Choose from expense categories:** food, travel, books, rent, fun,
    and other.
-   **View all saved expenses** in a readable list.
-   **See a spending summary**, including the total spent and the amount
    left in the budget.
-   **Compare spending by category**, with simple percentage bars.
-   **Identify the biggest single expense** in the current list.
-   **Get a budget warning** when total spending goes over the budget.
-   **Delete an expense** if you added it by mistake.
-   **Save data automatically** in `expenses.json`.

## ⚫ Technologies and Tools Used

  -----------------------------------------------------------------------
  Technology / Tool                   How it is used
  ----------------------------------- -----------------------------------
  **Python 3**                        Main programming language

  `json`                              Saves and loads expense data

  `os`                                Checks whether the data file exists

  `datetime.date`                     Adds the current date to each
                                      expense

  **Terminal / Command Prompt**       Runs the program and accepts user
                                      input

  **VS Code or another text editor**  Can be used to edit the Python file
  -----------------------------------------------------------------------

The project uses Python's built-in modules, so no extra packages are
required.

## 🟡 Installation and Setup

### 1. Install Python

Make sure Python 3 is installed on your computer. You can get it from
the official website:

<https://www.python.org/downloads/>

During installation on Windows, select **"Add Python to PATH"** if that
option appears.

### 2. Save the project file

Save the Python code as:

``` text
student_expenses.py
```

Keep the file inside a folder where you want the project and its saved
data to live.

### 3. Open a terminal

Open Command Prompt, PowerShell, or a terminal in your project folder.

### 4. Run the program

Use this command:

``` bash
python student_expenses.py
```

If your system uses the `python3` command, run:

``` bash
python3 student_expenses.py
```

### 5. Start tracking expenses

A menu will appear with these options:

``` text
=== Student Expense Tracker ===
1. Set budget
2. Add expense
3. View all expenses
4. Summary
5. Delete an expense
6. Quit
```

Enter the number for the action you want to perform and follow the
prompts.

> **Note:** The program creates `expenses.json` when it saves data for
> the first time. Keep this file if you want to preserve your saved
> budget and expenses.

## 🔴 How to Test the Project

There is no separate automated test suite included, so you can check the
main features manually using the steps below.

  ------------------------------------------------------------------------------
  Test                    What to do                     Expected result
  ----------------------- ------------------------------ -----------------------
  **Start the program**   Run                            The menu appears in the
                          `python student_expenses.py`   terminal

  **Set a budget**        Choose option `1` and enter    The budget is saved
                          `5000`                         

  **Add an expense**      Choose option `2`; enter       The expense is added
                          `Lunch`, category `food`, and  with today's date
                          amount `150`                   

  **View expenses**       Choose option `3`              The saved expense
                                                         appears in the list

  **Check summary**       Choose option `4`              Total spending and
                                                         category breakdown are
                                                         displayed

  **Check budget          Add expenses whose total       A message shows how
  warning**               exceeds the budget             much the budget has
                                                         been exceeded

  **Delete an expense**   Choose option `5` and enter    That expense is removed
                          the expense number             

  **Check saved data**    Quit and run the program again Previously saved data
                                                         is loaded from
                                                         `expenses.json`

  **Try invalid input**   Enter text where a number is   The program asks for
                          expected                       valid numeric input
  ------------------------------------------------------------------------------

For a clean test, you can make a backup of `expenses.json` before
experimenting. Only delete that file if you are happy to remove the
locally saved data.

## 🟡 Screenshots

Screenshots are not included yet. You can add your own terminal
screenshots here after running the program.

For example:

``` markdown
![Main Menu](screenshots/main-menu.png)
![Expense Summary](screenshots/expense-summary.png)
```

If you use these examples, create a `screenshots` folder in your project
and put the matching image files inside it.

## ⚫ Project Structure

After running the program for the first time, the folder may look like
this:

``` text
student-expense-tracker/
├── student_expenses.py
├── expenses.json
└── README.md
```

-   `student_expenses.py` --- the main Python program.
-   `expenses.json` --- the saved budget and expense records, created by
    the program.
-   `README.md` --- project information and instructions.

## 🔴 A Small Note

This is a basic, terminal-based project made for learning and personal
expense tracking. It keeps data locally in a JSON file and does not use
an online account or database.

## 🟡 Author

**Suyash Dixit**\
**University:** VIT Bhopal University\
**Branch:** Mechanical Engineering (AI and Robotics)

------------------------------------------------------------------------

::: {align="center"}
**🔴 Manage your money. 🟡 Understand your spending. ⚫ Spend
mindfully.**
:::


