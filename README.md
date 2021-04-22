# node-react
helping commands for node and react

### create node server
1. create package.json
2. ceate index.js
3. run ```npm start```


### Create React App
1. ```npm install -g create-react-app```
2. ```create-react-app app_name```
3. ```cd app_name```
4. ```npm start```
5. ```npm test```
6. npm run build (optional to run get build for react app)
7. write Dockerfile 
8. write docker-compose.yml file (docker volumes if you need runtime editing)


### Ways to Run Tests
1. Build docker image then run cmd ```docker run image-name -it npm run test```
2. for docker-compose firstly up containers then run cmd ```docker exec -it image-name npm run test```

> **_NOTE:_** To run tests automatically add command ```npm run test``` at last of service 

## Production Envoirnment
1. Added Multi-Step Dockerfile.prod with nginx
2. To build image cmd ```docker build -f Dockerfile.prod . ```
3. To run container cmd ``` docker run -p 80:80 --name node_app prod_frontend ```
