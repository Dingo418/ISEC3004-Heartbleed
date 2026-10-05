# Heartbleed Vulnerable Server for ISEC3004
This repository contains the proof-of-concept of the heartbleed exploit, vulnerable openssl server in a container and a mitigated container.
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

# One Liner

```bash
# 1. Clone the repo
git clone https://github.com/Dingo418/ISEC3004-Heartbleed. 
cd ISEC3004-Heartbleed

# 2. Build and run the vulnerable server
cd heartbleed_server
docker build -t heartbleed-server .
docker run -it --rm -p 8787:8787 heartbleed-server
cd ../

# 2. Build and run the vulnerable server
cd patched_heartbleed
docker build -t heartbleed-patched .
docker run -it --rm -p 8788:8788 heartbleed-patched
cd ../

# 3. Setup the exploit
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cd exploit

# 4. Run the exploit on the vulnerable server
python main.py -p 8787

# 5. Run the exploit on mitigated server
python main.py -p 8788
```
