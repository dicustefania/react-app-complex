Server ( express server) is listening on port 5000 ( configuration set in index.js)
Client ( react-app) is listening by default on port 3000.

Set NGINX that there is an 
- upstream server at client:3000
- upstream server at server:5000
- if anyone comes to '/' send them to client upstream
- if anyone comes to '/api' send them to server upstream
- we want to set that after the request with /api/values... comes to nginx 
to remove the /api and to remain only the request /values/.. send to the express server.
(because in the code the paths are set without /api)

Browser requests come to nginx .
Nginx does the routing between Client( react-app) or Server ( express server or api server).
React server communicate with Express Server.
Express Server communicate with Redis and Postgress. 
Redis communicates with worker.

Worker = does the fibbonaci calculation itself