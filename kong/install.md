```bash
docker pull kong
```
```bash
docker network create kong-net
```
```bash
docker run -d --name kong-database --network=kong-net -p 5432:5432 -e "POSTGRES_USER=kong" -e "POSTGRES_DB=kong" -e 
"POSTGRES_PASSWORD=kong" postgres:9.6
```
```bash
docker run -d --name kong --network=kong-net -e "KONG_DATABASE=postgres" -e "KONG_PG_HOST=kong-database" -e 
"KONG_CASSANDRA_CONTACT_POINTS=kong-database" -p 8000:8000 -p 8443:8443 -p 8001:8001 -p 8444:8444 kong
```


```bash
docker exec -it kong kong migrations bootstrap
```