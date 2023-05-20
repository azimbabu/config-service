# Containerize With Cloud Native Buildpacks
## Build OCI Image
```
 ./gradlew bootBuildImage
```
## Create Docker Network
```
docker network create catalog-network
```
## Run Container
```
docker run -d \                                                 
--name config-service \
--net catalog-network \
-p 8888:8888 \
--platform linux/amd64 \
config-service

```
## Cleanup
```
docker rm -f config-service

docker network rm catalog-network
```
## Build and Publish
```
./gradlew bootBuildImage \
--imageName=ghcr.io/azimbabu/config-service \
--publishImage \
-PregistryUrl=ghcr.io \
-PregistryUsername=azimbabu \
-PregistryToken=<PERSONAL-ACCESS-TOKEN>
```