# Heartbleed vulnerable server

# Get legacy Ubuntu Xenial Xerus due to build dependencies
FROM ubuntu:16.04

# Get all the dependencies for building OpenSSL
RUN apt-get update && \
    apt-get install -y build-essential git

# Latest release of openSSL with the Heartbleed vulnerability which is 1.0.1f
RUN git clone https://github.com/openssl/openssl.git && \
    cd openssl && \
    git checkout 96db9023b881d7cd9f379b0c154650d6c108e9a && \
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

# Start the vulnerable server on port 8788 with generated certificate
ENTRYPOINT /openssl/apps/openssl s_server -key key.pem -cert cert.pem -accept 8788 -www
