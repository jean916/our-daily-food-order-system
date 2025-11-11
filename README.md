# our-daily-food-order-system
A PL/SQL-based mini restaurant system for “Our Daily Food”, featuring order input, price calculation, and receipt display.


## Overview
**Our Daily Food** is a simple PL/SQL project that simulates how a restaurant handles customer orders.  
It demonstrates key PL/SQL programming concepts:
- **RECORDS** – to group related data (food name, price, quantity, total)
- **COLLECTIONS** – to store multiple records (several orders)
- **GOTO** – to handle invalid input by retrying

---

## Project Goal
The goal of this project is to show how PL/SQL can be applied to a real-life system:
1. Use **Records** and **Collections** to manage restaurant orders.  
2. Use **GOTO** to re-enter input when invalid data is provided.  
3. Calculate and print a simple receipt for the customer.

---

## How to Run the Project
1. Open **Oracle SQL Developer** or **Oracle Live SQL**.  
2. Copy the main PL/SQL script into a new worksheet.  
3. Run the script (Press **F5**).  
4. When asked for `Enter_Quantity`, type:
   - `0` → to test retry using `GOTO`
   - or any positive number → to calculate totals normally.

