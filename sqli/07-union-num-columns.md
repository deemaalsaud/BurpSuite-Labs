# Lab 07 – SQLi (UNION): Determine number of columns

Goal:
figure out how many columns the original query returns so a UNION attack will line up.

---
What I did (my way)
- even though the lab says it’s vulnerable, I still tossed a `'` in the category param to double-check.
- this page had a button flow, so I focused on column count first (don’t overthink the UI).
- used `ORDER BY` testing: ' ORDER BY 3-- and it gave me **200 OK**
- so i tried ' ORDER BY 4-- but it gave me an error
so there are 3 columns (tbh I could kind of tell from the page layout, but I verified it properly)

another solution 
without relying on errors, you can try matching column count with NULLs: ' UNION SELECT NULL,NULL,NULL--

- If it works (or changes the page slightly), that’s a good sign you hit the right number.
- If it errors, add/remove `NULL`s until it aligns (2, 3, 4…).

You can test data types later by swapping one `NULL` for a string example: ' UNION SELECT 'test',NULL,NULL--

## Notes
- i kinda knew it was 3 just by looking, but wanted to prove it with `ORDER BY`.  
- spent a minute overthinking the datatype part, then realized the lab only wanted column count.







