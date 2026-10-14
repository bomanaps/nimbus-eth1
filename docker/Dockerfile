FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y \
    ca-certificates curl build-essential git cmake \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /home/user/nimbus-eth1
COPY . .

RUN make -j$(nproc) nimbus
