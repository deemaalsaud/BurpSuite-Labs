# Lab 02 – SQLi: Login bypass

Goal:
log in as **administrator** without knowing the real password.

What I did:
- opened the login page from the lab  
- tried a normal login but failed
- caught the request in proxy
- in the username field I added: 'OR 1=1--
- lefy the password empty
- success !

Why it worked:
the `'` closes the original query,  
`OR 1=1` always makes the condition true,  
`--` comments out the rest (so the password check is ignored)

Notes
funny thing i didn’t even use Repeater, just Proxy.  

