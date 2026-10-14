FROM debian:bookworm-slim AS build

RUN apt-get update && apt-get install -y \
    ca-certificates curl build-essential git cmake \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /home/user/nimbus-eth1
COPY . .

RUN make -j$(nproc) nimbus

FROM debian:bookworm-slim

COPY --from=build /home/user/nimbus-eth1/build/nimbus /home/user/nimbus-eth1/build/nimbus
