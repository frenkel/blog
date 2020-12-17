---
layout: post
title: "Using gitlab-ci-multi-runner on OpenBSD"
date: 2016-04-06 21:14:22 +0200
comments: true
categories: OpenBSD
---

After contributing some small build problem fixes for `gitlab-ci-multi-runner` and two of it's dependencies, I've made it possible to run CI builds from Gitlab on OpenBSD. The following instructions will help you set it up yourself.
<!-- more -->

Installing dependencies
-----------------------
Gitlab-ci-multi-runner and the two dependency tools tools are written in Go, so we obviously need to install `go`. The other dependencies we need are `bash` (the runner uses it at runtime), `curl` and `gmake`.

Setting GOPATH correctly
------------------------
Go needs a place to store the source code and binaries. This can be configured using the GOPATH environment variable. This variable needs to be set in order for the instructions below to work. You can set it to a place in your homedirectory for example: `export GOPATH=~/gopath`.

Building go-bindata
-------------------
The first tool that we need it go-bindata. It is used to convert a prebuilt Docker image into Go source code, so that it can be embedded in the final `gitlab-ci-multi-runner` binary.

Build the tool using the following commands.

```
go get github.com/jteeuwen/go-bindata
cd $GOPATH/src/github.com/jteeuwen/go-bindata
go build -o $GOPATH/bin/go-bindata ./go-bindata
```

Building docker cli
-------------------
The docker client binary is needed next. Build it using the following commands.

```
go get github.com/docker/docker
cd $GOPATH/src/github.com/docker/docker
GOPATH=$GOPATH:`pwd`/vendor go build -o $GOPATH/bin/docker ./docker
```

Building gitlab-ci-multi-runner
-------------------------------
Finally, we can build the binary itself using the following commands.

```
go get gitlab.com/gitlab-org/gitlab-ci-multi-runner
cd $GOPATH/src/gitlab.com/gitlab-org/gitlab-ci-multi-runner
PATH=$PATH:$GOPATH/bin gmake docker
go build -o $GOPATH/bin/gitlab-ci-multi-runner ./main.go
```

Result
------
`$GOPATH/bin` should now contain `gitlab-ci-multi-runner`. Because Go programs are built statically, you can simply copy it to your other systems, install `bash` on them and start running your CI builds. How's that for deployment?
