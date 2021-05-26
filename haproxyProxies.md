






| Name  | Description |
| ------------- | ------------- |
| mode  | The running mode of the instance. Could be tcp, http or health. The first two are the most common. tcp operates on layer 4 & http operates on layer 7.  |
| backlog  | The number of connections waiting in line to be processed after maxconn has reached its limit.  |
| balance  | The algorithm to be used while trying to distribute the traffic over several servers. There are a couple of choices to be applied here, which you can find the names and the explanations of each in the doc.  |
| Compression  | The algorithm of the HTTP compression. |
| timeout  | The amount of timeout on different occasions. connect refers to the connection to the server, client which refers to the maximum inactivity time of the client, tarpit is the amount of time to maintain tarpitted connections, server is the maximum amount of inactivity time of the server.  |
| option  | This parameter has a lot of usages. forwardfor is used to add X-Forward-For header when delivering the traffic to the server.  |
