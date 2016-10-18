FROM ubuntu:xenial

# ENV must match the version in ubuntu:xenial at time of build
ENV CURL_VERSION=7.47.0
ENV CURL_UBUNTU_VERSION=1ubuntu2.1
#TODO: ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /tmp

RUN apt-get update \
    && apt-get -y build-dep curl \
    && apt-get -y install libnghttp2-dev \
    && apt-get -y source curl \
    && cd /tmp/curl-$CURL_VERSION \
    && debian/rules binary \
    && cd /tmp \
    && dpkg -i \
        curl_${CURL_VERSION}-${CURL_UBUNTU_VERSION}_amd64.deb libcurl3*.deb

# TODO: delete build deps and dev packages to slim down image size

USER nobody
CMD curl --http2 -I nghttp2.org
