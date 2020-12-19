# node-1

Below is the general infraestructure diagram.

![image](https://user-images.githubusercontent.com/76201917/102675558-7e347e00-415f-11eb-9aae-72472e43916a.png)

A user request site https://b.gvps.site

- DNS find the record and redirect to google cloud servers
- Compute instance receives the request
- Request is redirected to node-2 server
- Node-2 verifies the request is valid and redirect to internal LAN server
