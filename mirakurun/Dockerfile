ARG ARCH=
FROM ${ARCH}node:22.14.0-bookworm AS build
WORKDIR /app
ENV DOCKER=YES NODE_ENV=production

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends build-essential git && \
    git clone --depth 1 https://github.com/Chinachu/Mirakurun.git /app && \
    npm ci --include=dev && \
    npm run build && \
    npm ci --omit=dev && \
    npm install source-map-support

FROM ${ARCH}node:22.14.0-bookworm-slim
WORKDIR /app
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        make \
        cmake \
        gcc \
        g++ \
        pkg-config \
        pcscd \
        libpcsclite-dev \
        libccid \
        libdvbv5-dev \
        pcsc-tools \
        dvb-tools \
        build-essential libtool autoconf git automake && \
# libarib25
    git clone https://github.com/stz2012/libarib25.git /tmp/libarib25 && \
    cd /tmp/libarib25 && \
    cmake . && \
    make && \
    make install && \
    cd /app && \
    rm -rf /tmp/libarib25 && \
# recpt1
    git clone https://github.com/stz2012/recpt1 /tmp/recpt1 && \
    cd /tmp/recpt1/recpt1 && \
    ./autogen.sh && \
    ./configure --enable-b25 && \
    make && \
    make install && \
    cd /app && \
    rm -rf /tmp/recpt1 && \
    apt-get -y remove $DEV && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY --from=build /app /app

CMD ["./Mirakurun/docker/container-init.sh"]
EXPOSE 40772 9229
