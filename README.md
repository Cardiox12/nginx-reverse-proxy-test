# Small nginx reverse proxy experiment

This project is a small experiment of nginx reverse proxy experiment.

The project use three containers, **server**, **app1** and **app2**. The **server** container is used as a reverse proxy and is the only container exposed to the host to demonstrate that it will serve private resources (**app1** and **app2**).\
Two servers are configured with the following server names : 
- **app1.example.com** for **app1** container 
- **app2.example.com** for **app2** container.

## How to run the project
To run the project, run : `docker-compose up -d`

## How to test the reverse proxy

To test that the **reverse proxy** works as intended, there are two ways :

### Curl
With curl, we can pass the `Host` key within the header : `curl -H 'Host: app1.example.com' http://localhost:8080`\
You should see the response.

### Web browser
This method need an extra step, for the browser to use the `Host` key within the header, we'll need to add these hostnames within the `/etc/host` file.
Add the following lines to your `/etc/host` file :
```
127.0.0.1	app1.example.com
127.0.0.1	app2.example.com
```

When this is done, go to your favortie web browser and type the following url : `http://app1.example.com` and `http://app2.example.com`.\
You should see a page with **app1** or **app2** depending on the url.
