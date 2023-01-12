### To save docker images

```
docker save -o <path for generated tar file> <image name>
docker load -i <path to image tar file>

```


### Docker daemon configuration
```
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": false,
  "features": {
    "buildkit": true
  },
  "registry-mirrors": [
    "https://docker.iranrepo.ir",
    "https://dockerhub.ir",
    "https://registry.docker.ir",
    "https://docker.host:5000"
  ]
}
```

### To run docker in same network as machin
```
docker run --network="host" .......
```

### To mound volume in current directory
```
docker run -v $(pwd):/docker_directory/  ....
```

### To run docker detached mode
```
docker run -d ......
```

### To enter in runnig container 
```
docker exec -it sha_key [bash|sh]
```
### To run docker interactively
```
docker run -it .........
```
### Delete stoped containers 
```
docker container prune
```

### To delete dangling docker images
```
docker image prune
```
