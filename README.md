# Heartbleed Vulnerable Server for ISEC3005

## Build & Run server vulnerable to Heartbleed
Access it on [https://localhost:8787](https://localhost:8787/)
```bash
cd heartbleed_server
docker build -t heartbleed-server .
docker run -it --rm -p 8787:8787 heartbleed-server
```

## Exploiting Hearbleed
TODO

## Fixing Heartbleed
  
  hbtype = *p++;
  n2s(p, payload);
  pl = p;
  
Remove this part of the code and add 

if (1 + 2 + 16 > s->s3->rrec.length)
  hbtype = *p++;
  n2s(p, payload);
if (1 + 2 + payload + 16 > s->s3->rrec.length)
  pl = p;

The 1.0.1g fix adds two bounds checks before any of that data is used, first confirming the received record is even large enough to contain a valid heartbeat header, then confirming the claimed payload length doesn't exceed the actual received record length. If either check fails, the request is silently discarded.

When an attacker sends a heartbeat request claiming a payload length larger than what was actually transmitted

if (1 + 2 + payload + 16 > s->s3->rrec.length)
    return 0;
    
catches this mismatch immediately. The request is silently discarded before the server ever reaches the code that allocates a response buffer and copies payload data into it.
