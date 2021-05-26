

| Name  | Description |
| ------------- | ------------- |
| daemon  | Run the process in the background (recommended mode)  |
| description  | An explanation of the process. Also shown in the stats webpage  |
| maxconn  | Maximum number of per-process connections. After reaching this limit, every new connection either goes to the backlog or is dropped if that limit is reached too.  |
| uid & gid  | Set the process’ user-id & group-id. Requires a useradd beforehand if you plan to run it with a different user than your current ones. Because you have to run the haproxy binary with sudo, You should specify this parameter to avoid receiving the connections asroot  |
| hard-stop-after  | Maximum amount of time allowed to perform a soft clean-stop using SIGUSR1. After which the process will receive a SIGKILL.  |
| log <address> <facility>  | The destination where logs are expected to be received. localhost local0 is the default expected destination when logging in the same host as the one running haproxy. It would redirect every log to Syslog and you can easily access them as simple as running journalctl.  |
| log-send-hostname  | Set the hostname field in the Syslog header. You can either provide a custom string or leave the argument empty, which would be replaced by the hosts’ hostname.  |
| mworker-max-reloads | The maximum amount of time a worker can survive a reload before receiving a SIGTERM. This is much more useful when having multiple instances of haproxy running in master-worker mode.  |
|  nbthread |  Set the number of threads the process should run on. Only available if you specified the following option during build: USE_THREAD=1  |
| pidfile | Write the PIDs of all the daemons into this file |
| stats socket  | This makes it possible to bind statistics to a UNIX socket. All the options are the exact ones used in the bind keyword as well. /var/run/haproxy.sock is the path of the socket, mode is for setting the socket permission, expose-fd listeners makes it that another haproxy process will be able to read the socket, level user will only show non-sensitive stats, maxconn was explained earlier, name will be the title of the tab in your browser, tfo if allowed will be used to receive the response as early as possible (read more in the doc)  |

  
  
