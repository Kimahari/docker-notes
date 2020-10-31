# Swarm Basic Features and How to Use Them In Your Workflow

## Scaling Out with Overlay Networking

    docker network create --driver overlay mydrupal

    docker network ls

    docker service create --name psql --network mydrupal -e POSTGRES_PASSWORD=mypass postgres

    docker service ls

    docker service ps psql

    docker container logs psql TAB COMPLETION

    docker service create --name drupal --network mydrupal -p 80:80 drupal

    docker service ls

    watch docker service ls

    docker service ps drupal

    docker service inspect drupal

## Scaling Out with Routing Mesh

    docker service create --name search --replicas 3 -p 9200:9200 elasticsearch:2

    docker service ps search

## Using Secrets in Swarm Services

    docker secret create psql_usr psql_usr.txt

    echo "myDBpassWORD" | docker secret create psql_pass - TAB COMPLETION

    docker secret ls

    docker secret inspect psql_usr

    docker service create --name psql --secret psql_user --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_USER_FILE=/run/secrets/psql_user postgres

    docker service ps psql

    docker exec -it psql.1.CONTAINER NAME bash

    docker logs TAB COMPLETION

    docker service ps psql

    docker service update --secret-rm

## Using Secrets with Swarm Stacks

    vim docker-compose.yml

    docker stack deploy -c docker-compose.yml mydb

    docker secret ls

    docker stack rm mydb
