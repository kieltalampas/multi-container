Dockerize the MongoDB Service
'docker run --name mongodb --rm -d -p 27017:27017 mongo'

Dockerize the Node App
- create dockerfile
- change the localhost to 'host.docker.internal'
'docker build -t goals-node .'
'docker run --name goals-backend --rm -d -p 80:80 goals-node'

Dockerize front end (react)
- create dockerfile
- 'docker build -t goals-react .'
- 'docker run --name goals-frontend --rm -d -p 3000:3000 -it goals-react'

Adding Docker Network
- docker network create <network name>

- run mongo db again using the new network 'docker run --name mongodb --rm -d --network goals-net mongo'
- change the port to 'mongodb://mongodb:27017/course-goals' name of the container of mongodb

- build the backend image again 'docker build -t goals-node .'
- run the backend container again using network 'docker run --name goals-backend --rm -d -p 80:80 --network goals-net goals-node'


- build the front end image again 'docker build -t goals-react .'
- run the container 'docker run --name goals-frontend --rm -d -p 3000:3000 -it goals-react'