NGINX_VERSION=1.8.0
NSSM_VERSION=2.24

MAKENSIS=/e/pApps/PortableApps/NSISPortable/App/NSIS/makensis.exe

NGINX_LINK=http://nginx.org/download/nginx-$(NGINX_VERSION).zip
NGINX_PKG=nginx-$(NGINX_VERSION)

NSSM_LINK=http://nssm.cc/download/nssm-$(NSSM_VERSION).zip
NSSM_PKG=nssm-$(NSSM_VERSION)


BIN= ../build/nginx-service.exe

.PHONY: clean all $(BIN)

$(BIN): deps/$(NGINX_PKG)/* deps/$(NSSM_PKG)/*
	cp -r deps/$(NGINX_PKG)/* tmp/
	cp deps/$(NSSM_PKG)/win32/nssm.exe tmp/nssm.exe
	cp -r ../src/*  tmp/
	mv tmp/conf/nginx.conf tmp/conf/nginx.conf.orig
	cp -r ../add-on/* tmp/
	cd tmp && $(MAKENSIS) nginx.nsi
	mv tmp/nginx-service.exe $(BIN)

deps/$(NGINX_PKG)/*: deps/$(NGINX_PKG).zip
	rm -rf deps/$(NGINX_PKG)/
	unzip deps/$(NGINX_PKG).zip -d deps/

deps/$(NSSM_PKG)/*: deps/$(NSSM_PKG).zip
	rm -rf deps/$(NSSM_PKG)/
	unzip deps/$(NSSM_PKG).zip -d deps/

deps/$(NGINX_PKG).zip:
	cd deps/ && wget $(NGINX_LINK)

deps/$(NSSM_PKG).zip:
	cd deps && wget $(NSSM_LINK)

clean:
	rm -rf ../build/*
	rm -rf deps/*
	rm -rf tmp/*

all: clean $(BIN)
