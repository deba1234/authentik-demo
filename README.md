

# Simple demo app

Idea is to protect whoami app with Authentik SSO. All containers are "behind" Treafik proxy which utilise letsencrypt service for SSL.

So, plan is, when i try to acceess https://solution-space.org (whoiam app) to be redirect to Authentik SSO Login page where i will type my credentials. I everything pass well (my credentials are good), i expect to be redirected to the https://solution-space.org site (whoami).


Start 
```
docker-compose up -d

#or 

make up
```


## STATUS: IN PROGRESS - HAVE ISSUE WITH PROXY SERVER 

Main error: "Detected potential redirect loop" (authentik proxy) 


When i want to got to main app (hosted on domain : https://solution-space.org) i get the following issue in logs

```shell
authentik-proxy_1  | {"event":"/akprox/auth/traefik","host":"solution-space.org","level":"info","logger":"authentik.outpost.proxyv2.application","method":"GET","name":"whoami-provider","remote":"192.168.176.6:60102","request_protocol":"HTTP/1.1","request_useragent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36","runtime":"4.697","size":75,"status":307,"timestamp":"2022-01-24T18:35:51Z","upstream":""}
traefik            | time="2022-01-24T18:35:51Z" level=debug msg="Remote error http://authentik-proxy:9000/akprox/auth/traefik. StatusCode: 307" middlewareName=authentik@docker middlewareType=ForwardedAuthType
authentik-proxy_1  | {"event":"Detected potential redirect loop","level":"info","logger":"authentik.outpost.proxy.bundle","provider":"whoami-provider","timestamp":"2022-01-24T18:35:51Z"}
authentik-proxy_1  | {"event":"/akprox/auth/traefik","host":"solution-space.org","level":"info","logger":"authentik.outpost.proxyv2.application","method":"GET","name":"whoami-provider","remote":"192.168.176.6:60102","request_protocol":"HTTP/1.1","request_useragent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36","runtime":"2.765","size":75,"status":307,"timestamp":"2022-01-24T18:35:51Z","upstream":""}
traefik            | time="2022-01-24T18:35:51Z" level=debug msg="Remote error http://authentik-proxy:9000/akprox/auth/traefik. StatusCode: 307" middlewareType=ForwardedAuthType middlewareName=authentik@docker
authentik-proxy_1  | {"event":"Detected potential redirect loop","level":"info","logger":"authentik.outpost.proxy.bundle","provider":"whoami-provider","timestamp":"2022-01-24T18:35:51Z"}
authentik-proxy_1  | {"event":"/akprox/auth/traefik","host":"solution-space.org","level":"info","logger":"authentik.outpost.proxyv2.application","method":"GET","name":"whoami-provider","remote":"192.168.176.6:60102","request_protocol":"HTTP/1.1","request_useragent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36","runtime":"2.033","size":75,"status":307,"timestamp":"2022-01-24T18:35:51Z","upstream":""}

...
```




