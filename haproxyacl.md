
https://www.haproxy.com/blog/introduction-to-haproxy-acls/


## Formatting an ACL

1. a named ACL 

2. an anonymous or in-line ACL.


This ACL name can then be used with if and unless statements



you can chain multiple conditions together. ACLs listed one after another without anything in between will be considered to be joined with an and. 



The condition overall is only true if both ACLs are true.  

~~~
example : http-request deny if { path -i -m beg /api/ } { src 10.0.0.0/16 }
~~~


Adding an exclamation mark inverts a condition:

~~~
example : http-request deny if { path -i -m beg /api/ } !{ src 10.0.0.0/16 }
~~~


You can also define an ACL where either condition can be true by using ||:    

~~~
example :   http-request deny if { path -i -m beg /evil/ } || { path -i -m end /evil }
~~~


This allows you to combine ANDs and ORs (as well as named and in-line ACLs) to build more complicated conditions. 

~~~
example :  http-request deny if evil !{ src 10.0.0.0/16 }
~~~


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


## Matching methods

| name  | description |
| ------------- | ------------- |
| str | Perform an exact string match  |
| beg  | Check the beginning of the string with the pattern, so a sample of “foobar” will match a pattern of “foo” but not “bar”.  |
| end  | Check the end of a string with the pattern, so a sample of foobar will match a pattern of bar but not foo.  |
| sub  | A substring match, so a sample of foobar will match patterns foo, bar, oba.  |
| reg  | -The pattern is compared as a regular expression against the sample.Warning: This is CPU hungry compared to the other matching methods and should be avoided unless there is no other choice.  |
| found  | This is a match that doesn’t take a pattern at all. The match is true if the sample is found, false otherwise. This can be used to (as a few common examples) see if a header (req.hdr(x-foo) -m found) is present, if a cookie is set (cook(foo) -m found), or if a sample is present in a map (src,map(/etc/hapee-1.8/ip_to_country.map) -m found).  |
| len  | Return the length of the sample (so a sample of foo with -m len 3 will match)  |





## Redirecting a request with http-request redirect


1. http-request redirect location

The command http-request redirect location sets the entire URI. For example to redirect non-www domains to their www variant

allow for log-format rules, specified using the %[] syntax

~~~
example - http-request redirect location http://www.%[hdr(host)]%[capture.req.uri] unless { hdr_beg(host) -i www }
~~~

2. http-request redirect scheme

our ACL, hdr_beg(host) -i www, ensures that the client is redirected unless their Host HTTP header already begins with www.

The command http-request redirect scheme changes the scheme of the request while leaving the rest alone. This allows for trivial http-to-https redirect lines

~~~
example - redirect scheme https if !{ ssl_fc } 
~~~

3. http-request redirect prefix

our ACL !{ ssl_fc } checks whether the request did not come in over https.

The command http-request redirect prefix allows you to specify a prefix to redirect the request to. For example, the following line causes all requests that don’t have a URL path beginning with /foo to be redirected to /foo/{original URI here}.:

~~~
example - http-request redirect prefix /foo if !{ path_beg /foo/ }
~~~

4. http-response set-header

you could inject the Strict-Transport-Security header via http-response set-header




## Selecting a backend with use_backend

In HTTP mode

The use_backend line allows you to specify conditions for using another backend



In TCP mode

routing decisions for TCP mode traffic, for example directing traffic to a special backend if the traffic is SSL

~~~
tcp-request inspect-delay 10s
use_backend be_ssl if { req.ssl_hello_type gt 0 }

~~~



Note that for tcp-level routing decisions, when requiring data from the client such as needing to inspect the request, the inspect-delay statement is required to avoid HAProxy passing the phase by without any data from the client yet.


## Setting an HTTP header with http-request set-header

| First Header  | Second Header |
| ------------- | ------------- |
| add-header  | Content Cell  |
| set-header | Content Cell  |
| replace-header  | Content Cell  |
| del-header | Content Cell  |


## Changing the URL with http-request set-path



## Updating map files with http-response set-map



## Caching with http-request cache-use

allowing the caching of resources based on ACLs. This, along with http-response cache-store, allows you to store select requests in HAProxy’s cache system


## Using ACLs to block requests

http-request deny

http-request tarpit

http-request silent-drop
