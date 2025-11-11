# our-daily-food-order-system
A PL/SQL-based mini restaurant system for “Our Daily Food”, featuring order input, price calculation, and receipt display.


## Overview
Our Daily Food is a simple PL/SQL project that simulates how a restaurant handles customer orders.  
It demonstrates key PL/SQL programming concepts:
- RECORDS – to group related data (food name, price, quantity, total)
- COLLECTIONS** – to store multiple records (several orders)
- GOTO – to handle invalid input by retrying

---

## Project Goal
The goal of this project is to show how PL/SQL can be applied to a real-life system:
1. Use Records and Collections to manage restaurant orders.  
2. Use GOTO to re-enter input when invalid data is provided.  
3. Calculate and print a simple receipt for the customer.

---

## How to Run the Project
1. Open Oracle SQL Developer or Oracle Live SQL.  
2. Copy the main PL/SQL script into a new worksheet.  
3. Run the script (Press **F5**).  
4. When asked for `Enter_Quantity`, type:
   - `0` → to test retry using `GOTO`
   - or any positive number → to calculate totals normally.
  

### Codes for Our Daily Food – Simple Restaurant Order System

SET SERVEROUTPUT ON;

DECLARE
  -- Record for one food order
  TYPE order_rec IS RECORD (
    food_name VARCHAR2(30),
    price NUMBER,
    qty NUMBER,
    total NUMBER
  );

  -- Collection (to store many orders)
  TYPE order_list IS TABLE OF order_rec INDEX BY PLS_INTEGER;
  orders order_list;

  total_amount NUMBER := 0;
  count_orders NUMBER := 0;
  qty_input NUMBER;

BEGIN
  DBMS_OUTPUT.PUT_LINE('=== OUR DAILY FOOD RESTAURANT ===');

  <<get_qty>>
  qty_input := &Enter_Quantity;
  IF qty_input <= 0 THEN
    DBMS_OUTPUT.PUT_LINE('Invalid quantity! Try again.');
    GOTO get_qty;
  END IF;

  -- Add 3 sample foods
  count_orders := 3;

  orders(1).food_name := 'Rice & Chicken';
  orders(1).price := 3000;
  orders(1).qty := qty_input;

  orders(2).food_name := 'Chapati & Beans';
  orders(2).price := 1500;
  orders(2).qty := 2;

  orders(3).food_name := 'Juice';
  orders(3).price := 1000;
  orders(3).qty := 1;

  -- Calculate totals
  FOR i IN 1..count_orders LOOP
    orders(i).total := orders(i).price * orders(i).qty;
    total_amount := total_amount + orders(i).total;
  END LOOP;

  -- Display receipt
  DBMS_OUTPUT.PUT_LINE('--------------------------------');
  DBMS_OUTPUT.PUT_LINE('Food Name           Qty    Total');
  DBMS_OUTPUT.PUT_LINE('--------------------------------');
  FOR i IN 1..count_orders LOOP
    DBMS_OUTPUT.PUT_LINE(
      RPAD(orders(i).food_name, 18) || ' ' ||
      LPAD(orders(i).qty, 3) || '   ' ||
      LPAD(orders(i).total, 6)
    );
  END LOOP;

  DBMS_OUTPUT.PUT_LINE('--------------------------------');
  DBMS_OUTPUT.PUT_LINE('Grand Total: ' || total_amount || ' RWF');
  DBMS_OUTPUT.PUT_LINE('Thank you for ordering from Our Daily Food!');

END;
/








