


Reference links :

https://www.haproxy.com/blog/introduction-to-haproxy-acls/






## Advantages

Proxying both TCP (IPv4 & IPv6 sockets) & HTTP (gateway) traffics and flowing the traffic in both directions.

Offloading/Initiating SSL connections to ensure a secure connection.

Normalizing HTTP traffics to allow valid requests only.

Content-based switching allows deciding the server to handle the request.

Load balancing the Server on different packets/requests.

Regulating traffics to apply rate-limiting.

Protecting against DDoS by maintaining statistics on IP, URL, etc.

Observation point for network troubleshooting using informative logs.

HTTP compression offloading.

Caching proxy to return repetitive and valid responses.

You can control traffic , limiting the number of simultaneous connections

Providing protection from unauthorized traffic


## what it does 

Receive the traffic, either layer 4 (TCP) or layer 7 (HTTP)

Manipulate it somehow according to our config (e.g. changing a header, decompressing, offloading SSL, etc.)

Decide on the server that should receive the traffic

Receive the response from the server and after doing some of the above steps, deliver the response back to the client



## capabilities

compression algorithm

regex

cryptography

systemd integration





## Installation 

http://www.haproxy.org/#down

wget 'http://www.haproxy.org/download/2.2/src/haproxy-2.2.3.tar.gz'

tar xf haproxy-2.2.3.tar.gz

make clean

make install


If you received an error regarding missing a package or library

apt install libopenssl

apt install zlib1g-dev

apt install libcrypt-dev
