FROM golang:latest
MAINTAINER Anielkis Herrera <d76fe15e@opayq.com>

ENV VERSION 7e2b03e20f4ab74764e41833e7814a1661b7e4c2

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9

RUN sh -c "echo deb https://get.docker.com/ubuntu docker main /etc/apt/sources.list.d/docker.list"

RUN mkdir -p /var/cache/drone /var/lib/drone && apt-get update && apt-get install -yq mercurial git bzr libsqlite3-dev sqlite3 build-essential docker.io

RUN go get github.com/tools/godep &&  git clone git://github.com/drone/drone.git /go/src/github.com/drone/drone
WORKDIR /go/src/github.com/drone/drone
RUN git reset --hard ${VERSION} && git clean -fdx
RUN make deps && make && make install
ADD drone.toml /etc/drone/drone.toml

EXPOSE 80

CMD [ "/usr/local/bin/droned", "-config=/etc/drone/drone.toml"]
#"--port=\":80\"", "-datasource=\"/var/lib/drone/drone.sqlite3\"", "-log.debug=true", "-log.level=5", "-log.file=\"/var/log/drone.log\"" ]
