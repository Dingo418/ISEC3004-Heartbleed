# Heartbleed vulnerable server

# Get legacy Ubuntu Xenial Xerus due to build dependencies
FROM ubuntu:16.04

# Get all the dependencies for building OpenSSL
RUN apt-get update && \
    apt-get install -y build-essential git

# Latest release of openSSL with the Heartbleed vulnerability which is 1.0.1f
RUN git clone https://github.com/openssl/openssl.git && \
    cd openssl && \
    git checkout 0d8776344cd7965fadd870e361503985df9c45bb && \
    ./config && \
    make && \
    make install_sw

# Generate a self-signed certificate for the server to use
# -nodes removes the passphrase requirement
RUN /openssl/apps/openssl req -x509 -newkey rsa:2048 \
  -keyout key.pem \
  -out cert.pem \
  -days 365 \
  -nodes \  
  -subj "/CN=localhost"

EXPOSE 8787

# Start the vulnerable server on port 8787 with generated certificate
ENTRYPOINT /openssl/apps/openssl s_server -key key.pem -cert cert.pem -accept 8787 -www
