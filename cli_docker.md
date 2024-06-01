These are notes from dockerizing a django/wagtail application utilizing a single container for the app and a seperate container for the database.

# Build the Image
## Prep
```
python -m pip freeze > requirements.txt
```
Then add back python and wagtail if removed

## Run the Build Command
```
docker build -t {{app_name}} .
```

# Build the Network
You'd probably only do this once. Note the ID that is returned. 
```
docker network create {{ntw_name}}
```

# Make the Database
```
docker run --name some-postgres ^
	--network-alias mydatabasecontainer ^
	-e POSTGRES_PASSWORD={{secret}} ^
	-e POSTGRES_DB={{db_name}} ^
	-e POSTGRES_USER={{db_user}} ^
	-d postgres ^
	--network {{ntw_name}} ^
```
Collapsed version:
```
docker run --name some-postgres --network-alias mydatabasecontainer -e POSTGRES_PASSWORD={{secret}} -e POSTGRES_DB={{db_name}} -e POSTGRES_USER={{db_user}} -d postgres --network {{ntw_name}} 
```


# Run the Container
```
docker run --env-file ./.env --network {{ntw_name}} -p 127.0.0.1:3000:8000 {{app_name}}
```
``` 
docker run --network {{ntw_name}} {{app_name}}
```
optional -d to run in detached

# Troubleshooting

## Stop and Remove a Container
```
docker ps
```
```
docker stop <the-container-id>
```
```
docker rm <the-container-id>
```

## Issues with endpoint.sh file 
Likely line endings. To fix in VScode, hit Ctrl + Shft + P -> Change End of Line Sequence


# Other Raw Notes

https://hub.docker.com/_/postgres


# add -v portfolio-data:/var/lib/mysql ???

docker exec -it a8d97c23b373d2a2f4198004dcfb082d3826fa9b7fa4a8c586a09184fe32710d psql --user portfolio_user portfolio

docker run -dp 127.0.0.1:3000:3000 ^
  -w /app -v "%cd%:/app" ^
  --network portfolio ^
  -e MYSQL_HOST=mysql ^
  -e MYSQL_USER=root ^
  -e MYSQL_PASSWORD=secret ^
  -e MYSQL_DB=todos ^
  node:18-alpine ^
  sh -c "yarn install && yarn run dev"
  
 docker run -p 127.0.0.1:3000:3000 -w /app -v "%cd%:/app" --network portfolio
