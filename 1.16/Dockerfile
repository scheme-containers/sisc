# -*- mode: dockerfile; coding: utf-8 -*-
FROM debian:buster-slim AS build
RUN apt-get update && apt-get -y --no-install-recommends install \
      unzip \
      build-essential \
 && rm -rf /var/lib/apt/lists/*
WORKDIR /build
COPY checksum checksum
ADD http://prdownloads.sourceforge.net/sisc/sisc-1.16.6.jar sisc.jar
RUN sha256sum sisc.jar && sha256sum -c checksum
RUN unzip sisc.jar "sisc/*"
WORKDIR /build/sisc
RUN mvn install

FROM debian:buster-slim
COPY --from=build /usr/local/ /usr/local/
RUN ln -s sisc /usr/local/bin/scheme-banner
CMD ["scheme-banner"]
