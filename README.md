# node-1

Below is the general infraestructure diagram.

![image](https://user-images.githubusercontent.com/76201917/102675558-7e347e00-415f-11eb-9aae-72472e43916a.png)

A user request site https://b.gvps.site

- DNS find the record and redirect to google cloud servers
- Compute instance receives the request
- Request is redirected to node-2 server
- Node-2 verifies the request is valid and redirect to internal LAN server

Process explanation - internal

![image](https://user-images.githubusercontent.com/76201917/102677413-e7b88a80-4167-11eb-8d80-2d9a8273b542.png)

- Request arrives to node-1 port 443
- HAProxy receives request, it checks if it is a valid domain according to the config
- If YES forwards the traffic to node-2-haproxy else denies access.
- Request arrives to node-2 port 443
- HAProxy receives request, it checks if it is a valid domain according to the config
- If YES forwards the traffic to node-2-nginx port 444 else denies access.
- NGINX receives request at port 444 (Alternate to not use already bind port 443 from HAPROXY (Same server))
- NGINX sends the hostname and domain to DNS to receive internal IP (DNSMASQ has a DHCP with all the internal IP's used)
- If DNS finds a match it will resolve the host to the internal IP
- NGINX forwards the request to the internal host
- If connection is succesful it will dispplay the web content, else it will return a 400 error handled by node-2-nginx



