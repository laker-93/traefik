# Set up

1. create cloudflare account
2. pay for cloudflar domain (e.g. sub-box.net)
3. Set up dns as shown in screen shot (separate subdomain for each docker service)
4. ensure CF is set to full encryption mode
5. set up port forwarding from router to local machine (HTTP, HTTPS, 8080)
6. use docker-compose attached
7. edit docker-compose with your CF email and global API token
8. services accessible from internet at:
    i. slskd.sub-box.net
    ii. navidrome.sub-box.net
    iii. sub-box.net (dashboard)
9.accessible locally:
    i. https://localhost/slskd
    ii. https://localhost/navidrome
    iii. http://localhost:8080/dashboard/#/http/routers


# Troubleshooting



    Browser throws ERR_TOO_MANY_REDIRECTS when accessing a service: If you deployed using CloudFlare's DNS servers and set CF to 'Flexible mode' then you will incurr in this error. This is because you have https from the client to the CF proxy, and forced http between the CF proxy and the server (forced by CF). As Traefik was configured with an http-to-https redirection itself, this will cause an infinite loop of redirects. In order to solve this issue, you need to set CF to Full encryption mode, and even without LE (using Traefik's self signed certificate) your website/application is now accessible.

    Browser throws ERR_SSL_VERSION_OR_CIPHER_MISMATCH when accessing a service: I ran into this error because the "edge certificates" (the certificates sitting at CloudFlare's proxy) did not have the same coverage for the routes I was setting up with Traefik.
        I was setting up routes with the structure service.platform.your-domain.com. This is called a 4th level subdomain.
        The "edge" certificates provided by CloudFlare (the "edge" being CF's proxy) only provide SSL up to 3rd level subdomains, specifically, to your-domain.com and *.your-domain.com.
        Thus the LE certificates fetch by Traefik did not match the names "made available" by CloudFlare, and the error above was produced.
        The only solution is to upgrade to a Enterprise subscription to CloudFlare 💸, as this allows you to issue edge certificates for any level of subdomains you want.

