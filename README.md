1. create a local registry for docker images:

```sh
docker service create --name registry --publish published=5000,target=5000 registry:2
```


2. test by local stack:

```sh
docker-compose up --build
```

now open browser and browse http://127.0.0.1:8080 to check the application.

after test the local stack can be removed by:

```sh
docker-compose down --volumes
```

3. push the images to registry for production deoployment:

```sh
docker-compose push
```

4. now start the stack on production swarm cluster:

```sh
docker stack deploy -c docker-compose.yml app
```

check the app with browser. it should be working now.

follwing commands can be used to check stack or individual services:

```sh
docker stack ls
docker stack ps app
docker service ls
docker service ps app_web
docker service inspect app_web
```

5. scale the application out by:

```sh
docker service scale app_web=5
```

check in browser to make sure the load balancing works fine.

6. to clear the environment:

```sh
docker stack rm app
docker service rm registry
```



