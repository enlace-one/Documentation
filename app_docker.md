This walks through setting up a django docker app.


# Dockerfile
In the main directory, add a `Dockerfile`

Example: 
```dockerfile
# Use an official Python runtime based on Debian 10 "buster" as a parent image.
FROM python:3.8.1-slim-buster

# Add user that will be used in the container.
RUN useradd wagtail

# Port used by this container to serve HTTP.
EXPOSE 8000

# Set environment variables.
# 1. Force Python stdout and stderr streams to be unbuffered.
# 2. Set PORT variable that is used by Gunicorn. This should match "EXPOSE"
#    command.
ENV PYTHONUNBUFFERED=1 \
    PORT=8000\
    DB_NAME=portfolio\
    DB_USER=portfolio_user\
    DB_HOST=portfoliodb

# Install system packages required by Wagtail and Django.
RUN apt-get update --yes --quiet && apt-get install --yes --quiet --no-install-recommends \
    build-essential \
    libpq-dev \
    libmariadbclient-dev \
    libjpeg62-turbo-dev \
    zlib1g-dev \
    libwebp-dev \
 && rm -rf /var/lib/apt/lists/*

# Install the application server.
RUN pip install "gunicorn==20.0.4"

# Install the project requirements.
COPY requirements.txt /
RUN pip install -r /requirements.txt

# Use /app folder as a directory where the source code is stored.
WORKDIR /app

# Set this directory to be owned by the "wagtail" user. This Wagtail project
# uses SQLite, the folder needs to be owned by the user that
# will be writing to the database file.
RUN chown wagtail:wagtail /app

# Copy the source code of the project into the container.
COPY --chown=wagtail:wagtail . .

# Use user "wagtail" to run the build commands below and the server itself.
USER wagtail

# Collect static files.
RUN python manage.py collectstatic --noinput --clear



# chmod fails if I don't switch to root
USER root
# Migrate and make super user
ADD docker-entrypoint.sh /docker-entrypoint.sh
# COPY docker-entrypoint.sh .
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
USER wagtail

# Runtime command that executes when "docker run" is called, it does the
# following:
#   1. Migrate the database.
#   2. Start the application server.
# WARNING:
#   Migrating database at the same time as starting the server IS NOT THE BEST
#   PRACTICE. The database should be migrated manually or using the release
#   phase facilities of your hosting platform. This is used only so the
#   Wagtail instance can be started with a simple "docker run" command.
#   removed: python manage.py migrate --noinput;
CMD ["set", "-xe", "gunicorn", "portfolio.wsgi:application"]
```

# .env
In the main directory, add a `.env` file.
```env
DJANGO_SUPERUSER_PASSWORD=
DJANGO_SUPERUSER_EMAIL=
DJANGO_SUPERUSER_USERNAME=django_superuser
DB_NAME=my_db
DB_USER=my_db_user
DB_PASSWORD=
DB_HOST=my_db_host
DB_PORT=5432
```

# Add a docker-entrypoint.sh
In the main directory, add a `docker-entrypoint.sh` file.
```sh
#!/bin/sh

python manage.py makemigrations --noinput
python manage.py migrate --noinput
# python manage.py createcachetable --noinput

if [ "$DJANGO_SUPERUSER_USERNAME" ]
then
    python manage.py createsuperuser \
        --noinput \
        --username $DJANGO_SUPERUSER_USERNAME \
        --email $DJANGO_SUPERUSER_EMAIL
fi

python manage.py runserver 0.0.0.0:8000
```

# .dockerignore
In the main directory, add a `.dockerignore` file.

Use a template made for your app, such as python/django. 