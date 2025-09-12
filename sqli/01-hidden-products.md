# Lab 01 – SQLi: Retrieve hidden products  

Goal:  
make the shop show the hidden products by messing with the category filter  

What I did: 
- opened the lab in burp’s browser  
- clicked a category → saw the request in http history  
- sent it to repeater  
- changed the value to = ' OR 1=1--
- sent the request -> boom hidden products

why it worked?
the site just drops whatever i type straight into a SQL query.  
no safety checks, so my lil trick forced it to return everything.   

How to fix it:
- use parameterized queries  
- don’t just glue user input into SQL  
- validate category input  

Notes :)
first sql injection lab i tried. it was fun!
