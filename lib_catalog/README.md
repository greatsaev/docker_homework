# What have been done to make it work

## Tune lib_catalog/settings.py

`USE_TZ = False`

## Tune requirements.txt

`lxml==4.5.2`
`psycopg2-binary>=2.8.6`

## Create app.sh
```
#!/bin/sh
sleep 10 && python manage.py migrate
python manage.py runserver 0.0.0.0:8000
```

# RUN
`docker network create backend`

`docker run --name database -e POSTGRES_PASSWORD=django -e POSTGRES_USER=django -p 5432:5432 --network backend  -d postgres:alpine3.14`

`docker run -d -p 8000:8000 --name backend --network backend backend`

Check that all migrations are done:

`docker logs backend`

Open *http://localhost:8000/admin* 