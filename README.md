# Burp Suite Labs

This repo is just me practicing **PortSwigger Web Security Academy labs** using Burp Suite.  
I’m keeping everything here so I can track my progress and have notes to look back on later.  

## How it’s organized
- Every vulnerability type has its own folder (SQLi, XSS, Auth, CSRF, etc).
- Inside each folder, I’ll add the labs I’ve done with simple write-ups.
- Each write-up = what the lab was, how I solved it, and what I learned.

## Index

### SQL Injection (SQLi)
- [01 – Hidden products](sqli/01-hidden-products.md)
- [02 – Login bypass](sqli/02-login-bypass.md)
- [03 – DB type/version (Oracle)](sqli/03-db-version-oracle.md)
- [04 – DB type/version (MySQL & Microsoft)](sqli/04-db-version-mysql-mssql.md)
- [05 – SQLi: Listing the database contents (non-Oracle)](sqli/05-list-db-contents-non-oracle.md)
- [06 – SQLi: Listing the database contents (Oracle)](sqli/06-list-db-contents-oracle.md)
- [07 – SQLi (UNION): Determine number of columns](sqli/07-union-num-columns.md)
- [08 – SQLi (UNION): Find a column containing text](sqli/08-union-find-text-column.md)
- [09 – SQLi (UNION): Retrieving data from other tables](sqli/09-union-retrieve-other-tables.md)
- [10 – SQLi (UNION): Retrieving multiple values in a single column](sqli/10-union-concat-single-column.md)
- [11 – Blind SQLi (conditional responses)](sqli/11-blind-conditional.md) — boolean-based blind extraction (length + substring/ASCII).










---

## How I write each lab
- **Goal** → what the lab wanted me to do  
- **Steps** → what I tried, payloads, and how I solved it  
- **Evidence** → screenshot or notes showing it worked  
- **Why it was vulnerable** → the root cause in plain English  
- **Fix** → how it *should* be fixed  
- **Notes** → anything that confused me or tips for myself later  

---

⚠️ **Disclaimer:** These are only practice labs from PortSwigger’s Academy.  
Don’t try this stuff on real websites without permission.
