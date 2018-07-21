# mmedica_docker
# Dockerized posgresql for Asseco mMedica

1 Create volume to store database files:
```
docker volume create pgdata_mmedica
```

2 Build postgres image for docker:
```
docker build -t postresql_mmedica mmedica
```
3 Start container:
```
docker run -p 5432:5432 --name mmedica_postgres -d -v pgdata_mmedica:/var/lib/postgresql/data postresql_mmedica
```
4 Enjoy
