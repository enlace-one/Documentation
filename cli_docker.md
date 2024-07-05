These are notes from dockerizing a django/wagtail application utilizing a single container for the app and a seperate container for the database.

# Just Docker

## First Time

### Build the Network
You'd probably only do this once. Note the ID that is returned. 
```
docker network create {{ntw_name}}
```

## On Cold Starts

### Run the Database
#### Without a .env file
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
docker run --name some-postgres --network-alias mydatabasecontainer -v {{local_volume}}:{{container_volume}} -e POSTGRES_PASSWORD={{secret}} -e POSTGRES_DB={{db_name}} -e POSTGRES_USER={{db_user}} -d postgres --network {{ntw_name}} 
```
My example:
```
docker run --name portfoliodb --network portfolio --network-alias portfoliodb -v C:\Docker\pgdev:/var/lib/postgresql/data -e POSTGRES_PASSWORD={{PG_PW}} -e POSTGRES_DB=portfolio -e POSTGRES_USER=portfolio_user -d postgres
```
#### With a .env file
Alternatively, you can store the database name, username, and password in a .env file. I decided on postgres.env so it would not clash with the app .env file. Here is my example:
```
docker run --name portfoliodb --network portfolio --network-alias portfoliodb -v C:\Docker\pgdev:/var/lib/postgresql/data --env-file ./postgres.env -d postgres
```

## Build the App Image

### Prep
```
cd /{{project_directory}}
```
```
./activate.bat
```
My example:
```
cd "OneDrive\Documents\Python\portfolio\portfolio" & "scripts/activate.bat"
```
#### Update Requirements
Only do if there is a requiremnets change.
```
python -m pip freeze > requirements.txt
```
Then add back python and wagtail if removed

### Run the Build Command
```
docker build -t {{app_name}} .
```
My example:
```
docker build -t portfolioapp .
```

## Run the App Container
### If container does not exist
```
docker run --env-file ./.env --network {{ntw_name}} -p 8000:8000 {{app_name}}
```
My example:
``` 
docker run --env-file ./.env --network portfolio -p 8000:8000 portfolioapp
```
Add an optional -d to run in detached
### If container does exist
Get the container name
```
docker ps -a
```
Start it 
```
docker start [name]
```

## Troubleshooting

### Stop and Remove a Container
```
docker ps
```
```
docker stop {{the_container_id}}
```
```
docker rm {{the_container_id}}
```

### Issues with endpoint.sh file 
Likely line endings. To fix in VScode, hit Ctrl + Shft + P -> Change End of Line Sequence

### Run Commands Inside a Container
```
docker exec -it {{db_container_id}} {{the_command}} --user {{user}}
```
1. `docker exec` Runs a command inside the docker container
2. `-it` keeps it open for interaction

#### Run PSQL inside the Database Container
```
docker exec -it {{db_container_id}} psql --user {{db_user}} {{db_name}}
```

# Docker Compose
## Build, Up, Down
You may get tired of all the commands. Follow app_docker.md to make a docker-compose.yml file then use these.

Build:
```
docker-compose --file docker-compose-dev.yml build
```
Up (optional -d for detached):
```
docker-compose --file docker-compose-dev.yml up
```
Down:
```
docker-compose down
```

# Sources

https://hub.docker.com/_/postgres

