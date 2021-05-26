
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



| name  | description  |
| ------------- | ------------- |
| src  | Returns the client IP address that made the request |
| path  | Returns the path the client requested  |
| url_param(foo)  | Returns the value of a given URL parameter |
| req.hdr(foo)  | Returns the value of a given HTTP request header (e.g. User-Agent or Host) |
| ssl_fc  | A boolean that returns true if the connection was made over SSL and HAProxy is locally deciphering it
Converters  |


## Converters

| name  | description  |
| ------------- | ------------- |
| lower  | Changes the case of a sample to lowercase  |
| upper | Changes the case of a sample to uppercase  |
| base64  | Base64 encodes the specified string (good for matching binary samples  |
| field  | Allows you to extract a field similar to awk. For example if you have “a|b|c” as a sample and run field(|,3) on it you will be left with “c”  |
| bytes  | Extracts some bytes from an input binary sample given an offset and length as arguments |
| map  | Looks up the sample in the specified map file and outputs the resulting value  |


## Flags

put multiple flags in a single ACL

| name  | description |
| ------------- | ------------- |
| -i  | Perform a case-insensitive match (so a sample of FoO will match a pattern of Foo)  |
| -f  | Instead of matching on a string, match from an ACL file. This ACL file can have lists of IP’s, strings, regexes, etc. As long as the list doesn’t contain regexes, then the file will be loaded into the b-tree format and can handle lookups of millions of items almost instantly  |
| -m  | Specify the match type. This is described in detail in the next section |
