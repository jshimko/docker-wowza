

# docker-wowza 

A Dockerfile to build a [Wowza Streaming Engine](http://www.wowza.com/products/streaming-engine) server.

**NOTE**: By using this image you are agreeing to comply with the [Wowza EULA](http://www.wowza.com/resources/WowzaStreamingEngine-4.0.0_LicenseAgreement.pdf)

Current Version: **4.1.2**

## Installation

```bash
git clone https://github.com/jshimko/docker-wowza.git
cd docker-wowza
docker build --tag="$USER/wowza:latest" .
```

## Usage

```bash
docker run --name='wowza' -d \
  -e 'WOWZA_KEY=xxxx-xxxx-xxxx-xxxx-xxxx-xxxx-xxxx' \
  -p 1935:1935 -p 8086:8086 -p 8087:8087 -p 8088:8088 \
  $USER/wowza:latest
```

Go to `http://DOCKER-HOST:8088` and login using the default username and password:

* username: **admin**
* password: **admin**

Refer to the wowza [quickstart guide](http://www.wowza.com/forums/content.php?3-quick-start-guide) for wowza configuration instructions.

## Volumes

The Wowza image is configured to save all configurations at `/data`. As such we should mount a volume at `/data`.

```bash
docker run --name='wowza' -d \
  -e 'WOWZA_KEY=xxxx-xxxx-xxxx-xxxx-xxxx-xxxx-xxxx' \
  -p 1935:1935 -p 8086:8086 -p 8087:8087 -p 8088:8088 \
  -v /opt/wowza:/data \
  $USER/wowza:latest
```

Upon the first run the image will copy all configurations to this location so you can persist configurations across container lifetimes.

## Shell

```bash
docker exec -it wowza bash
```

## Upgrading

To upgrade the image, you need to rebuild the image from the latest source and do the following.

- **Step 1**: Stop and remove the running container

```bash
docker stop wowza
docker rm wowza
```

- **Step 2**: Start the updated image

```bash
docker run --name=wowza -d [OPTIONS] $USER/wowza:latest
```

## References

  * http://www.wowza.com/products/streaming-engine
