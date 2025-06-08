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

WITH AUTH
ENV MONGODB_USERNAME=root
ENV MONGODB_PASSWORD=secret
- change the port to `mongodb://${process.env.MONGODB_USERNAME}:${process.env.MONGODB_PASSWORD}$@mongodb:27017/course-goals?authSource=admin` name of the container of mongodb
- run mongo db again using the new network `docker run --name mongodb -v data:/data/db --rm -d --network goals-net -e MONGO_INITDB_ROOT_USERNAME=kiel -e MONGO_INITDB_ROOT_PASSWORD=secret mongo`

WITHOUT AUTH
- change the port to `mongodb://mongodb:27017/course-goals`
- run mongo db again using the new network `docker run --name mongodb -v data:/data/db --rm -d --network goals-net mongo` 
- build the backend image again `docker build -t goals-node .`
- run the backend container again using network `docker run --name goals-backend --rm -d -p 80:80 --network goals-net goals-node' or 'docker run --name goals-backend --rm -p 80:80 --network goals-net goals-node` attached mode


- build the front end image again `docker build -t goals-react .`
- run the container `docker run --name goals-frontend --rm -d -p 3000:3000 -it goals-react`

VOLUMES for BACKEND
- stop the backend container
- run backend again with volumes and live changes using nodemon
- add devDependencies
- change docker file 'CMD ["npm", "start"]'
- rebuild image

WITHOUT AUTH
- `docker run --name goals-backend -v C:\Users\User\Downloads\multi-01-starting-setup\multi-01-starting-setup\backend:/app -v logs:/app/logs -v /app/node_modules -d --rm -p 80:80 --network goals-net goals-node`

WITH AUTH
- `docker run --name goals-backend -v C:\Users\User\Downloads\multi-01-starting-setup\multi-01-starting-setup\backend:/app -v logs:/app/logs -v /app/node_modules -e MONGODB_USERNAME=kiel -d --rm -p 80:80 --network goals-net goals-node`


VOLUMES FOR FRONTEND
- `docker run -v C:\Users\User\Downloads\multi-01-starting-setup\multi-01-starting-setup\frontend\src:/app/src --name goals-frontend --rm -p 3000:3000 -it goals-react`