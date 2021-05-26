

a backend and a frontend is that the traffic received from the user is always delivered firstly to the frontend.

No backend is directly accessible by any traffic sent from the user unless a frontend captures the packet first.

“listen” acts as both frontend and backend in which it is accessible by the user and it forwards the traffic to the server as well.



| Name | Description |
| ------------- | ------------- |
| bind  | Specify the address to bind to, which will expose a port on the host on either of the network interfaces it has |
| maxconn & backlog | are the same as the ones used in the global section.  |
| stats  | Has a couple of parameters to configure the statistical reports. auth is for specifying a username & a password for viewing the page, enable is used to activate the stats reports, show-legends is to show additional information on the page, uri is the prefix to append when trying to view the page. I have provided a sample report at the end of the article so that you’ll get a good feeling of how it operates.  |
| server  | This is used to specify the IP addresses of each server. The balance parameter explained earlier is used here to distribute between servers you specify here.  |
