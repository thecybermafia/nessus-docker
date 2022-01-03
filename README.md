
## Nessus Vulnerability Scanner for arm64 
* Checkout the code using
```
$ git clone https://github.com/thecybermafia/nessus-docker
$ cd nessus-docker
```
### Getting the latest version of Nessus 

1. Get the latest installer `Nessus-<latest-version>-ubuntu1110_amd64.deb` and place it inside the `nessus-scanner` directory
2. Modify the filename on `line #12` inside `Dockerfile` to match the downloaded file i.e. `Nessus-<latest-version>-ubuntu1110_amd64.deb`

### Cross-Platform Buildx Build

* Execute below commands to build docker image using buildx and load it, you can also use `--push` switch to push the built images
```
docker buildx build -f Dockerfile --platform linux/amd64 . --load
```
```
WARN[0000] invalid non-bool value for BUILDX_NO_DEFAULT_LOAD:  
[+] Building 12.2s (12/12) FINISHED                                                                                                                                             
 => [internal] load build definition from Dockerfile                                                                                                                       0.0s
 => => transferring dockerfile: 564B                                                                                                                                       0.0s                              
 => [internal] load .dockerignore                                                                                                                                          0.0s                              
 => => transferring context: 2B                                                                                                                                            0.0s                              
 => [internal] load metadata for docker.io/library/ubuntu:16.04                                                                                                            1.3s                              
 => [1/6] FROM docker.io/library/ubuntu:16.04@sha256:0f71fa8d4d2d4292c3c617fda2b36f6dabe5c8b6e34c3dc5b0d17d4e704bd39c                                                      0.0s
 => => resolve docker.io/library/ubuntu:16.04@sha256:0f71fa8d4d2d4292c3c617fda2b36f6dabe5c8b6e34c3dc5b0d17d4e704bd39c                                                      0.0s                              
 => [internal] load build context                                                                                                                                          0.0s                              
 => => transferring context: 58B                                                                                                                                           0.0s                              
 => CACHED [2/6] RUN apt-get update                                                                                                                                        0.0s                              
 => CACHED [3/6] RUN apt-get install -y net-tools iputils-ping tzdata                                                                                                      0.0s                              
 => CACHED [4/6] RUN rm -rf /var/lib/apt/lists/*                                                                                                                           0.0s                              
 => CACHED [5/6] COPY Nessus-10.0.2-ubuntu1110_amd64.deb /tmp/Nessus.deb                                                                                                   0.0s                              
 => CACHED [6/6] RUN dpkg -i /tmp/Nessus.deb                                                                                                                               0.0s                              
 => exporting to oci image format                                                                                                                                         10.8s                              
 => => exporting layers                                                                                                                                                    6.4s
 => => exporting manifest sha256:fe0eef329e2b8bbf495f062b192ba090bbf261d059d5a31c56d29de9f5d28299                                                                          0.0s
 => => exporting config sha256:8b66cd8145ebce639b757acbb97ed2e5cc4b52003d0dead2c33857d01df6757a                                                                            0.0s                              
 => => sending tarball                                                                                                                                                     4.4s
 => importing to docker                                                                                                                                                    3.1s
                                                                                   
```

* Execute below commands to view list of images
```
docker image ls
```
```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              8b66cd8145eb        3 minutes ago       559MB
```

### Running the generated image

* Execute below commands to run the docker container
```
docker run -d -p 8834:8834 8b66cd8145eb
```
* Execute below commands to check if the container is running
```
docker ps
```
```                  
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                       PORTS                    NAMES
5eda12c204d9        8b66cd8145eb        "/opt/nessus/sbin/ne…"   16 seconds ago      Up 15 seconds                0.0.0.0:8834->8834/tcp   vibrant_wescoff
```

* If the container has successfully started, we can access it from browser using https://localhost:8834
* Follow the steps to activate and create accounts
* Note: Compiling the plugins might take some significant time

* We can login to the container using below command after getting the id from `docker ps` command

```
docker exec -it 5eda12c204d9 bash
```
