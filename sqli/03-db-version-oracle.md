# Lab 03 – SQLi: Querying DB type & version (Oracle)

Goal: 
figure out what database type/version the app is running (Oracle in this case).

What I tried: 
- intercepted the request in Burp  
- knew this one was trickier than just `' OR 1=1--`  
- Oracle uses a different syntax than MySQL/Postgres  
- tried playing with UNION SELECT and version functions  
- ngl it was confusing, I peeked at hints/solution
- the trick was using Oracle’s special `DUAL` table with a UNION SELECT  


' UNION SELECT 'a','b' FROM DUAL-- 

Notes: felt a lot harder than Lab 1 & 2.
i didn’t fully solve it without looking, will need to redo later when I understand UNION + Oracle syntax
