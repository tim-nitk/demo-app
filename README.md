## Demo web application proposal 


Hey there ya'll , I decided to make a readme cuz its tough to format messages on fleep.  


Anyways, so there is this `docker-compose.yaml` 

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
**without using kubectl** :P

I think that's it for now :) WIll be updated with more details if necessary

Output on my local machine - 

![image info](https://i.ibb.co/s19WMpt/boring-todo-list.png)

Alrighty !
until next time:)

---------------------------

Fun fact:


`tmaddy69/todo-app` is actually my own image (no pun intended) so if anybody is interested in really customizing it you can feel free to *fleep* me. 

I basically built it off of [Keystone JS](https://www.keystonejs.com/) using the `keystone-app` tool available in npm . Dockerfile has been documented [here](https://www.keystonejs.com/guides/deployment/#docker). of course I had to [`cookieSecret`](https://www.keystonejs.com/guides/production/#cookie-secret) cuz that's a MUST HAVE in production environemnt.

Mongodb `adapterURI` should now point to the mongodb://mongo:270127/my-sample-db 

✌️
