Hey there ya'll , I decided to make a gist cuz its tough to format messages on fleep 
anyways so there is this `docker-compose.yaml` 

```yaml

version: '3.8'
services:
  app:
    container_name: app-container
    restart: always
    image: tmaddy69/todo-app
    ports:
      - "3000:3000"
    depends_on:
      - mongo
  mongo:
    container_name: mongo-backend
    image: mongo
    expose:
      - "27017"
    ports:
      - "27017:27017"
    volumes:
      - apiDB:/data/db

volumes:
  apiDB:

```

Its a multi container app that uses 2 images (pre-exisitng on docker hub)

`app`: node server that implements CRUD api 
`mongo`: the actual database where the stuff is stored


Steps to run them on your machine (if you have docker installed)

1. Create the file `docker-compose.yaml` and paste the above yaml code
2. Then run the command `docker-compose up -d` 
3. (optional) Check the status of the containers with `docker ps`
4. Now hop onto `http://localhost:3000/`


Steps to deploy on Kubernetes

- Since its a milti-container app we can first install [kompose](https://kompose.io/) to make our lives easy !

1. Create the file `docker-compose.yaml` and paste the above yaml code
2. `kompose convert`
3. `kubectl apply -f *.yaml`
4. `kubectl get po`

but of course.... we bootstrapped our own kubernetes so I am not entirely sure how to get around 
*wihtout using kubectl* :P

I think that's it for now :) WIll be updated with more details if necessary

Output on my local machine - 

![image info](https://i.ibb.co/s19WMpt/boring-todo-list.png)
