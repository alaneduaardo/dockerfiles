FROM golang:latest
MAINTAINER Anielkis Herrera <d76fe15e@opayq.com>

ENV VERSION 7354ad8e95b4d068f28ae448e1a163fcbb320cdf

RUN mkdir -p /var/cache/drone /var/lib/drone && apt-get update && apt-get install -yq mercurial git bzr libsqlite3-dev sqlite3 build-essential

RUN go get github.com/tools/godep &&  git clone git://github.com/drone/drone.git /go/src/github.com/drone/drone
WORKDIR /go/src/github.com/drone/drone
RUN git reset --hard ${VERSION} && git clean -fdx
RUN make deps && make && make install
ADD drone.toml /etc/drone/drone.toml

EXPOSE 80

CMD [ "/usr/local/bin/droned", "-config=/etc/drone/drone.toml"]
#"--port=\":80\"", "-datasource=\"/var/lib/drone/drone.sqlite3\"", "-log.debug=true", "-log.level=5", "-log.file=\"/var/log/drone.log\"" ]
