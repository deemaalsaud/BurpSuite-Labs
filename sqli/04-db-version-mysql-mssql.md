# Lab 04 – SQLi: Querying DB type & version (MySQL & Microsoft)

Goal:
figure out the database type/version when the backend is MySQL or Microsoft SQL.

What I did: 
- first i tested if its vulnerable to SQL injection by just typing ' in category
- intercepted the request that sets the product category filter in Burp & sent it to repeater 
- determine the number of columns using order by clause, there are 2 columns 
- used a test payload: ' UNION SELECT 'abc','def'# this showed both columns accept string data  
- then swapped in a payload to grab the version: ' UNION SELECT @@version, NULL#

Notes:
this one felt smoother because I understood the UNION flow better after Lab 03.
