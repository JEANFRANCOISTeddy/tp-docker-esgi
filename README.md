# tp-docker-esgi

Create bidged network :

    docker network create -d bridge --subnet=172.1.1.0/24 my-bridge-network

Deploy a Nginx container on MyBridgedNetwork :

    docker run -d -it --network MyBridgedNetwork --name web nginx

Deploy a mongo container on MyBridgedNetwork :

    docker run -d -it --network MyBridgedNetwork --name db mongo


Attach a volume “bdd” to the mongo container :

    docker volume create bdd

    docker run -d --network MyBridgedNetwork --name bdd mongo --mount source=bdd,destination=/bdd

Create a second network named BCNetwork 172.2.2.0/24 :

    docker network create -d bridge --subnet=172.2.2.0/24 BCNetwork

Deploy an Ethereum node on a container on BCNetwork that you will have built and pushed on dockerhub beforehand (dockerfile to support).

    docker volume create blockchain

    docker build -t geth ./geth

    docker run -d -it --network BCNetwork --mount source=blockchain,destination=/blockchain --name geth geth

Run docker compose :

    docker-compose up --build