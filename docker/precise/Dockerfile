FROM ubuntu:precise

ENV DEBIAN_FRONTEND noninteractive

ENV GOLANG_VERSION 1.5.2
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA1 cae87ed095e8d94a81871281d35da7829bd1234e

ENV GOPATH /usr/share/gocode
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN apt-get update -qq && apt-get dist-upgrade -qq -y \
  && apt-get install -qq --no-install-recommends -y \
    build-essential ubuntu-dev-tools debhelper devscripts \
    libdistro-info-perl libparse-debcontrol-perl \
    git curl

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA1  golang.tar.gz" | sha1sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

COPY deps/ /tmp
RUN dpkg -i /tmp/*.deb
