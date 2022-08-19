# New Makefile for multi-architecture - 仅本地构建，不涉及docker
.PHONY: all

CODEPATH := ../
VERSION ?= $(shell date +'%Y%m%d%H%M%S')
VERSION := $(VERSION)


PLATFORMS=linux
ARCHITECTURES=amd64

all: resource-server.build.amd64 build-zgctl-all-platforms

all.amd64: resource-server.build.amd64

# USING BUILD AND UPLOAD INSTEAD OF IMAGE AND PUSH TO AVOID COLLISION
resource-server.build.amd64:
	@mkdir -p $(CODEPATH)docker/dist/amd64
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/reaper $(CODEPATH)cmd/reaper/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/jobexecutor $(CODEPATH)cmd/jobexecutor/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/aslan $(CODEPATH)cmd/aslan/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/config $(CODEPATH)cmd/config/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/cron $(CODEPATH)cmd/cron/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/hub-agent $(CODEPATH)cmd/hub-agent/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/hub-server $(CODEPATH)cmd/hub-server/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/picket $(CODEPATH)cmd/picket/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/podexec $(CODEPATH)cmd/podexec/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/policy $(CODEPATH)cmd/policy/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/ua $(CODEPATH)cmd/ua/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/user $(CODEPATH)cmd/user/main.go
	@CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -v -o $(CODEPATH)docker/dist/warpdrive $(CODEPATH)cmd/warpdrive/main.go

pre-build:
	@mkdir -p $(CODEPATH)bin/

build-zgctl-all-platforms: pre-build
	$(foreach GOOS, $(PLATFORMS),\
	$(foreach GOARCH, $(ARCHITECTURES), $(shell export GOOS=$(GOOS); export GOARCH=$(GOARCH); CGO_ENABLED=0 go build -v -o $(CODEPATH)bin/zgctl-$(GOOS)-$(GOARCH) $(CODEPATH)cmd/zgctl/main.go)))


.PHONY: clean
clean:
	@rm -rf $(CODEPATH)docker/dist
	@rm -rf $(CODEPATH)bin/
