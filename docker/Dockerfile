FROM debian:bookworm-slim AS build

RUN apt-get update && apt-get install -y \
    ca-certificates curl build-essential git cmake \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /nimbus-eth1
COPY . .

RUN make -j$(nproc) nimbus

FROM debian:bookworm-slim AS deploy

RUN apt-get update && apt-get install -y jq curl \
    && rm -rf /var/lib/apt/lists/*

COPY --from=build /nimbus-eth1/build/nimbus /usr/bin/nimbus
RUN /usr/bin/nimbus --version > /version.txt

COPY docker/genesis.json /genesis.json
COPY docker/mapper.jq /mapper.jq
COPY docker/nimbus.sh /nimbus.sh
RUN chmod +x /nimbus.sh
COPY docker/enode.sh /hive-bin/enode.sh
RUN chmod +x /hive-bin/enode.sh

EXPOSE 8545 8546 8547 8551 30303 30303/udp
ENTRYPOINT ["/nimbus.sh"]
