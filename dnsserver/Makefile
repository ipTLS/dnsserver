piSSHAddress ?= pi@192.168.0.126
version ?= 0.0.0
module=dnsserver
outfile=./bin/$(module)-$(1)-$(2)-$(version)
test_opts=

define build_arch_os
	GOARCH=$(1) GOOS=$(2) go build -o "$(outfile)"
	chmod a+x "$(outfile)"
endef

build: build_linux build_darwin build_arm

build_arm:
	$(call build_arch_os,arm,linux)
build_linux:
	$(call build_arch_os,amd64,linux)
build_darwin:
	$(call build_arch_os,amd64,darwin)
test_arm: build_arm
	scp -r "$(outfile)" ${piSSHAddress}:./Downloads/
	ssh ${piSSHAddress} sudo Downloads/"$(outfile)" ${test_opts}
test_darwin: build_darwin
	"$(outfile)" ${test_opts}
release: build