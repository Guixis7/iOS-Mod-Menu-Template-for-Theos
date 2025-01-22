# THEOS_DEVICE_IP = 127.0.0.1 -p 2222 # install to device from pc
ARCHS = arm64 #arm64e
DEBUG = 0
STRIP =:
FINALPACKAGE = 1
FOR_RELEASE = 1

# 0 to treat warnings as errors, 1 otherwise.
IGNORE_WARNINGS=1

#THEOS_PACKAGE_SCHEME = rootless

TARGET := iphone:clang:latest:11.0

## Common frameworks ##
PROJ_COMMON_FRAMEWORKS = UIKit Foundation Security QuartzCore CoreGraphics CoreText

## source files ##
KITTYMEMORY_SRC = $(wildcard KittyMemory/*.cpp)
SCLALERTVIEW_SRC =  $(wildcard SCLAlertView/*.m)
MENU_SRC = Menu.mm

include $(THEOS)/makefiles/common.mk

FRAMEWORK_NAME = FFH4XJOBCheats

FFH4XJOBCheats_FILES = FFH4XJOBCheats.m
FFH4XJOBCheats_PUBLIC_HEADERS = FFH4XJOBCheats.h
FFH4XJOBCheats_INSTALL_PATH = /Library/Frameworks
FFH4XJOBCheats_CFLAGS = -fobjc-arc
FFH4XJOBCheats_LDFLAGS += API/libAPIClient.a
FFH4XJOBCheats_CCFLAGS = -std=c++11 -fno-rtti -fno-exceptions -DNDEBUG

ifeq ($(IGNORE_WARNINGS),1)
FFH4XJOBCheats_CFLAGS += -w
FFH4XJOBCheats_CCFLAGS += -w
endif

FFH4XJOBCheats_FILES = Tweak.xm $(MENU_SRC) $(KITTYMEMORY_SRC) $(SCLALERTVIEW_SRC)

FFH4XJOBCheats_LIBRARIES += substrate

FFH4XJOBCheats_FRAMEWORKS = $(PROJ_COMMON_FRAMEWORKS)
# GO_EASY_ON_ME = 1

include $(THEOS_MAKE_PATH)/framework.mk
include $(THEOS_MAKE_PATH)/tweak.mk

internal-package-check::
	@chmod 777 versionCheck.sh # Give permission to script 	
	@./versionCheck.sh # Script to verify template's current version

after-install::
	install.exec "killall -9 @@BINARYNAME@@ || :"
