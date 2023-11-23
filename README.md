This project is based on: https://github.com/fjudith/docker-draw.io/tree/master/self-contained
I have added the traefik part for self signed certificate and reverse proxy


1. Download this project
2. Generate certificate and private key for your drawio server (check [this guide](https://gist.github.com/KeithYeh/bb07cadd23645a6a62509b1ec8986bbc))
3. Paste the content of it inside `./secrets/drawio.lab.lan-crt.pem` and `./secrets/drawio.lab.lan-crt.pem`
4. Edit the line ```- "traefik.http.routers.drawio.rule=Host(`drawio.iss.lan`)"``` from docker-compose and change the dns name according to your setup.
6. Run the compose: `docker compose up -d`

`docker ps` result:

```
CONTAINER ID   IMAGE                      COMMAND                  CREATED          STATUS          PORTS                                           NAMES
ef9dc2e31b3c   jgraph/drawio              "/docker-entrypoint.…"   26 minutes ago   Up 26 minutes   8080/tcp, 8443/tcp                              drawiov2-drawio-1
2f71039c9373   traefik:2.10.5             "/entrypoint.sh --pr…"   26 minutes ago   Up 26 minutes   80/tcp, 0.0.0.0:443->443/tcp, :::443->443/tcp   drawiov2-traefik-1
a5e8b5e902fc   plantuml/plantuml-server   "/entrypoint.sh"         36 minutes ago   Up 36 minutes   8080/tcp                                        drawiov2-plantuml-server-1
c277e543cc5c   jgraph/export-server       "docker-entrypoint.s…"   36 minutes ago   Up 36 minutes   8000/tcp                                        drawiov2-image-export-1
```

Screenshots

<img width="963" alt="image" src="https://github.com/s0p4L1n3/Drawio-traefik-TLS-compose/assets/126569468/ec309206-d6c5-4065-8fef-e2636483b007">
