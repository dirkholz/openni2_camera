all: openni2_driver

GIT_DIR = openni2_src
GIT_URL=-b develop git://github.com/dirkholz/OpenNI2.git
#GIT_REVISION=eb90cb8583ff40f95fc22e45d87898f40bf425d6

include $(shell rospack find mk)/git_checkout.mk

openni2_driver_build: download
	cd $(GIT_DIR) && \
	make && \
	cd Packaging && ./ReleaseVersion.py x64 && \
	cd ../..

openni2_driver: openni2_driver_build 
	$(eval ONI_DIR=`pwd`/$(GIT_DIR)/Packaging/`ls $(GIT_DIR)/Packaging/ | grep OpenNI-`)
	echo $(ONI_DIR) && \
	mkdir -p include/openni2 && mkdir -p lib && \
	cp -r $(ONI_DIR)/Include/* ./include/openni2/ && \
	cp -r $(ONI_DIR)/Redist/* ./lib/ && \
	cp ./cfg/OpenNI.ini ./lib/ && \
	cp ./cfg/PS1080.ini ./lib/OpenNI2/Drivers

clean: 
	rm -rf $(GIT_DIR) patched build include lib rospack_nosubdirs
