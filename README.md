
# Devaten_Middleware

This middleware was created to have an easy-to-set-up link between Devaten and Prometheus.

This middleware helps you, the user, monitor your database. Through Devaten and Prometheus, all the relevant information about different tasks performed on your database will be monitored and saved, and this information is easily accessible through the Prometheus and Devaten dashboard.

Further down this document, you can find a guide on how to install, run and use this middleware.

You must have a Devaten account to use this middleware. You can create an account on their [website](https://app.devaten.com/).

## How to Install

To install the middleware locally, you must have git, docker, and docker-compose installed:

To get the Middleware Docker Compose File you have to clone the git Middleware Repository using the following:

https://github.com/devatengit/middleware.git

Once the clone is completed you got a middleware folder on your system. Go inside the folder you received three files. 
[ docker-compose.yml, Prometheus and middleware.env ]  

## How to Run

Go inside the cloned folder named middleware which contains the above three files.

Open Command Prompt and run command ```docker-compose pull```  

This will download the docker images locally.

Then run ```docker-compose up```


## How to Use

When the docker image is running, it is running on the local port **8999**, which is the port you can use to start and stop a Devaten recording.

We expose 2 ports for Prometheus. The first is **9090** which is where the "targets" and "graph" for **Prometheus** are located. Also, the image will open the port **9091** that can be used to access information about the recording through **Prometheus.**

The image will export Grafana on port **3000**.

Once the middleware is up and running, you can do the following API calls, API calls can be made through the address-bar in the browser:

### Login

```
localhost:8999/Login/{Devaten Username}/{Devaten Password}
```
eg. localhost:8999/Login/abc@gmail.com/123456

This call must be made as the first API call, or it will not be possible to start or stop a recording.

Once you have logged in, you can start and stop recordings without having to log in again.

If the image is ever shut down, you must log in again when you restart the program.

### Start Recording

```
localhost:8999/Start/{Usecase name}/{Application Identifier}
```

**Usecase name** can be anything that you choose.

**Application Identifier** can be found in Devaten, under *Applications* and *Application Management.*

### Stop Recording

```
localhost:8999/Start/{Usecase name}/{Application Identifier}
```

**Usecase name** has to be the same as the name used to start the recording.

**Application Identifier** has to be the same as the application identifier used to start the recording.


## **Prometheus**

*Please remember to login before hand. See subsection [Login](#login)*
Access prometheus dashboard (in browser) on path:http://mymiddelware.localhost:9090/ 

Access Devaten custom metrics in txt format on path: http://localhost:9091/metrics

## **Grafana**

Access Grafana on path: http://localhost:3000/

*OBS! Beware that first time users of Grafana needs to login with credentials: {uname}: admin, {password}: admin

## How to Stop Containers

```docker-compose down```