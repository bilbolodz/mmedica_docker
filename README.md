# mmedica_docker
Dockerized posgresql for Asseco mMedica

Create volume to store database files:

docker volume create pgdata_mmedica

Build postgres image for docker:

docker build -t postresql_mmedica mmedica

Start container:

docker run -p 5432:5432 --name mmedica_postgres -d -v pgdata_mmedica:/var/lib/postgresql/data postresql_mmedica

Enjoy
