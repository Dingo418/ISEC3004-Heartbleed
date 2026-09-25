# Heartbleed Vulnerable Server for ISEC3004

## Build & Run server vulnerable to Heartbleed
Access it on [https://localhost:8787](https://localhost:8787/)
```bash
cd heartbleed_server
docker build -t heartbleed-server .
docker run -it --rm -p 8787:8787 heartbleed-server
```

## Build & Run server with Heartbleed mitigated
Access it on [https://localhost:8788](https://localhost:8788/)
```bash
cd patched_heartbleed
docker build -t heartbleed-patched .
docker run -it --rm -p 8788:8788 heartbleed-patched
```


## Exploiting Hearbleed
Setup:
```bash
pip install -r requirements.txt
cd exploit
```

Perform exploit on vulnerable machine:
```bash
python main.py -p 8787
```

Perform exploit on patched machine/
```bash
python main.py -p 8788
```