Dockerize the MongoDB Service
'docker run --name mongodb --rm -d -p 27017:27017 mongo'

Dockerize the Node App
- create dockerfile
- change the localhost to 'host.docker.internal'
'docker build -t goals-node .'
'docker run --name goals-backend --rm -d -p 80:80 goals-node'