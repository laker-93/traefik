1. create cloudflare account
2. pay for cloudflar domain (e.g. sub-box.net)
3. Set up dns as shown in screen shot (separate subdomain for each docker service)
4. set up port forwarding from router to local machine (HTTP, HTTPS, 8080)
5. use docker-compose attached
6. services accessible from internet at:
    1. slskd.sub-box.net
    2. navidrome.sub-box.net
    3. sub-box.net (dashboard)
7.accessible locally:
    1. https://localhost/slskd
    2. https://localhost/navidrome
    3. http://localhost:8080/dashboard/#/http/routers
