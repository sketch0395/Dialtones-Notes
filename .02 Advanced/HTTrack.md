## Install Httrack

```BASH
sudo apt install httrack

httrack <site> -O <nameoffile>

```
## Create Docker Image

### Create Docker File in site
- Create ```Dockerfile``` within website directory
- Within ```Dockerfile``` Import lightweight web server
``` Shell
FROM nginx
COPY . /usr/share/nginx/html
```

- Build docker container and run
``` Docker 
docker build -t <Target_Name> <Target_folder_path>
docker run -it -d -p 8080:80 <target_name>
```

- Stop docker
```Shell
# Find running container id
docker ps -a -f status=running
# Tell it to stop
docker stop -t 60 <container id>
```
