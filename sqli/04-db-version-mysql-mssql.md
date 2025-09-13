# Lab 04 – SQLi: Querying DB type & version (MySQL & Microsoft)

Goal:
figure out the database type/version when the backend is MySQL or Microsoft SQL.

What I did: 
- intercepted the request that sets the product category filter in Burp  
- tested how many columns the query expected, used ORDER BY tricks and UNION SELECT  
- confirmed it was returning 2 columns, both text  
- used a test payload: ' UNION SELECT 'abc','def'# this showed both columns accept string data  
- then swapped in a payload to grab the version: ' UNION SELECT @@version, NULL#

Notes:
this one felt smoother because I understood the UNION flow better after Lab 03.
