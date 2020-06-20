Following https://tutorialedge.net/golang/go-docker-tutorial/

- Dockerfile specifies the config to build the image
- main.go is a very simply web app
-- run locally using go run main.go // exposed on localhost:8081
-- or 
-- build and tag an image using ... docker build -t my-go-app .

(note: manually typing docker build is OK ... but using a docker-compose up is better)

Output in terminal :
    ➜  go-docker docker build -t my-go-app .
    Sending build context to Docker daemon  4.096kB
    Step 1/6 : FROM golang:1.12.0-alpine3.9
    1.12.0-alpine3.9: Pulling from library/golang
    8e402f1a9c57: Pull complete 
    ce7779d8bfe3: Pull complete 
    de1a1e452942: Pull complete 
    1bdc943bc000: Pull complete 
    a8c461e224a6: Pull complete 
    Digest: sha256:6c143f415448f883ed034529162b3dc1c85bb2967fdd1579a873567b22bcb790
    Status: Downloaded newer image for golang:1.12.0-alpine3.9
    ---> 2205a315f9c7
    Step 2/6 : RUN mkdir /app
    ---> Running in cb25d7c81caa
    Removing intermediate container cb25d7c81caa
    ---> 5d2597d5cdb0
    Step 3/6 : ADD . /app
    ---> 15f14a3dd06e
    Step 4/6 : WORKDIR /app
    ---> Running in 7e35c20e5198
    Removing intermediate container 7e35c20e5198
    ---> 4629c2359280
    Step 5/6 : RUN go build -o main .
    ---> Running in 92556f431498
    Removing intermediate container 92556f431498
    ---> 56de1476c78f
    Step 6/6 : CMD ["/app/main"]
    ---> Running in d0c879b735eb
    Removing intermediate container d0c879b735eb
    ---> 330a40bdeae1
    Successfully built 330a40bdeae1
    Successfully tagged my-go-app:latest

Next steps ...
- docker images ... shows the new image saved locally, 350MB
- docker run -p 8080:8081 -it my-go-app
    instanciates and runs a _container_ locally, mapping container 8081 to local 8080

Even cooler ... spin up three my-go-app containers mapped to 3 local ports:
- docker run -d -p 8080:8081 -it my-go-app
- docker run -d -p 8082:8081 -it my-go-app
- docker run -d -p 8084:8081 -it my-go-app

Kill them ... use docker ps to get container ID or NAMES
- docker ps
- docker stop abff48a6b31d e92430ccb1fa 2075cf49a08a
- docker ps // verify all have spun down 

