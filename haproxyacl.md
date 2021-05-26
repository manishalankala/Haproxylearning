
https://www.haproxy.com/blog/introduction-to-haproxy-acls/


## Formatting an ACL

1.a named ACL 

2. an anonymous or in-line ACL.


This ACL name can then be used with if and unless statements



you can chain multiple conditions together. ACLs listed one after another without anything in between will be considered to be joined with an and. 



The condition overall is only true if both ACLs are true.     example : http-request deny if { path -i -m beg /api/ } { src 10.0.0.0/16 }

Adding an exclamation mark inverts a condition:               example : http-request deny if { path -i -m beg /api/ } !{ src 10.0.0.0/16 }

You can also define an ACL where either condition can be true by using ||:     example :   http-request deny if { path -i -m beg /evil/ } || { path -i -m end /evil }

This allows you to combine ANDs and ORs (as well as named and in-line ACLs) to build more complicated conditions. example :  http-request deny if evil !{ src 10.0.0.0/16 }



## fetch

A source of information in HAProxy is known as a fetch

--- | ----
