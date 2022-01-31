Server ( express server) is listening on port 5000 ( configuration set in index.js)
Client ( react-app) is listening by default on port 3000.


Browser requests arrive to nginx. Nginx is mapped as 3050:80 ( see docker-compose.yml). Locally: localhost:3050/

Set NGINX to have:
- upstream server at client:3000
- upstream server at server:5000
- if anyone comes to '/' send them to client upstream
- if anyone comes to '/api' send them to server upstream
- we want to set that after the request with /api/values... comes to nginx 
to remove the /api and to remain only the request /values/.. send to the express server.
(because in the code index.js of server the paths are set without /api)

Nginx does the routing between Client( react-app) or Server ( express server or api server) (see default.conf)
React server communicate with Express Server. ( with request like /api/values.. from Fib.js) And Express Server sees them as /values/.. ( see in index.js)
Express Server communicate with Redis and Postgress. ( in keys.js some varaibles are set for connection and we defined them as environment variables in docker-compose) 
Worker communicates with redis. (in index.js and keys.js-- but why we don't define keys like for server in docker-compose ??) 

Worker = does the fibbonaci calculation itself