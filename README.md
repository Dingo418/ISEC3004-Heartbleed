# Heartbleed Vulnerable Server for ISEC3004

## Build & Run server vulnerable to Heartbleed
Access it on [https://localhost:8787](https://localhost:8787/)
```bash
cd heartbleed_server
docker build -t heartbleed-server .
docker run -it --rm -p 8787:8787 heartbleed-server
```

## Build & Run server with Heartbleed mitigated
Access it on [https://localhost:8787](https://localhost:8787/)
```bash
cd heartbleed_server/patched_heartbleed
docker build -t heartbleed-patched -f Dockerfile.patched .
docker run -it --rm -p 8787:8787 heartbleed-patched
```


## Exploiting Hearbleed
TODO
