# Lab 08 – SQLi (UNION): Find a column containing text

**Goal:**  
figure out which column in the UNION output accepts text, so I can print strings later.

---

## What I did
- this lab is basically **part 2** of the previous one (Lab 07).  
- already knew the query had 3 columns.  
- lab gave me a test string: `'jyOVdY'`.  

so I tested each column one by one: ' UNION SELECT 'jyOVdY',NULL,NULL-- gave me an error.
' UNION SELECT NULL,'jyOVdY',NULL-- worked !

## Notes:
this lab was a nice confidence boost 

