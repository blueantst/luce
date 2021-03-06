
LUCE_SQUISH_DIR = ../../luce_squishable

MAKEFLAGS += --no-print-directory

VERSION = $(shell git describe)
OUT 	= distrib

TARGETS_51_ := linux64 win32 osx64 ios61 android44
TARGETS_51 := $(foreach obj,$(TARGETS_51_),$(OUT)/$(VERSION)/luce.$(VERSION).$(obj)-5.1.zip)
TARGETS_52_ := linux64 win32
TARGETS_52 := $(foreach obj,$(TARGETS_52_),$(OUT)/$(VERSION)/luce.$(VERSION).$(obj)-5.2.zip)

LUCE_LIB   := $(OUT)/$(VERSION)/luce.lua


all:
	echo "It's $$(date)"

distrib: $(LUCE_LIB) $(TARGETS_51) $(TARGETS_52)

lua51: $(LUCE_LIB) $(TARGETS_51)

lua52: $(LUCE_LIB) $(TARGETS_52)

$(LUCE_LIB): $(LUCE_SQUISH_DIR)
	@cd $^ && make extraclean && make
	@mkdir -p $(OUT)/$(VERSION)
	@\cp -af $^/luce.lua $(OUT)/$(VERSION)/


$(OUT)/$(VERSION)/Linux64/build: Linux $(LUCE_LIB)
	@echo Building for Linux64 5.1
	@mkdir -p $(shell dirname $(@))/luce
	@cp -f $(OUT)/$(VERSION)/luce.lua $(shell dirname $(@))/
	@cd $< && make -j5 && make -j5 CONFIG=Debug
	@ln -f $</build/core.so $(@:build=luce/core.so)
	@ln -f $</build/core_d.so $(@:build=luce/core_d.so)
	@ln -f $</build/intermediate/Release/libluce_lin.a $(@:build=luce/libluce.a)
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).linux64-5.1.zip luce/core.so luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).linux64-5.1_dbg.zip luce/core_d.so luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).linux64-5.1_static.zip luce/libluce.a luce.lua

$(OUT)/$(VERSION)/luce.$(VERSION).linux64-5.1.zip: $(OUT)/$(VERSION)/Linux64/build \
												   $(OUT)/$(VERSION)/Linux64/luce/core.so \
												   $(OUT)/$(VERSION)/Linux64/luce/core_d.so \
												   $(OUT)/$(VERSION)/Linux64/luce/libluce.a \
												   $(OUT)/$(VERSION)/Linux64/luce.lua \
												   $(OUT)/$(VERSION)/luce.$(VERSION).linux64-5.1_dbg.zip \
												   $(OUT)/$(VERSION)/luce.$(VERSION).linux64-5.1_static.zip

linux64: $(OUT)/$(VERSION)/luce.$(VERSION).linux64-5.1.zip

$(OUT)/$(VERSION)/Linux64-5.2/build: Linux-lua5.2 $(LUCE_LIB)
	@echo Building for Linux64-5.2 5.2
	@mkdir -p $(shell dirname $(@))/luce
	@cp -f $(OUT)/$(VERSION)/luce.lua $(shell dirname $(@))/
	@cd $< && make -j5 && make -j5 CONFIG=Debug
	@ln -f $</build/core.so $(@:build=luce/core.so)
	@ln -f $</build/core_d.so $(@:build=luce/core_d.so)
	@ln -f $</build/intermediate/Release/libluce_lin.a $(@:build=luce/libluce.a)
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).linux64-5.2.zip luce/core.so luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).linux64-5.2_dbg.zip luce/core_d.so luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).linux64-5.2_static.zip luce/libluce.a luce.lua

$(OUT)/$(VERSION)/luce.$(VERSION).linux64-5.2.zip: $(OUT)/$(VERSION)/Linux64-5.2/build \
												   $(OUT)/$(VERSION)/Linux64-5.2/luce/core.so \
												   $(OUT)/$(VERSION)/Linux64-5.2/luce/core_d.so \
												   $(OUT)/$(VERSION)/Linux64-5.2/luce/libluce.a \
												   $(OUT)/$(VERSION)/Linux64-5.2/luce.lua \
												   $(OUT)/$(VERSION)/luce.$(VERSION).linux64-5.2_dbg.zip \
												   $(OUT)/$(VERSION)/luce.$(VERSION).linux64-5.2_static.zip

linux64-5.2: $(OUT)/$(VERSION)/luce.$(VERSION).linux64-5.2.zip

$(OUT)/$(VERSION)/Win32/build: MingW $(LUCE_LIB)
	@echo Building for Win32 5.1
	@mkdir -p $(shell dirname $(@))/luce
	@cp -f $(OUT)/$(VERSION)/luce.lua $(shell dirname $(@))/
	@cd $< && ./wrapper && ./wrapper debug
	@ln -f $</build/core.dll $(@:build=luce/core.dll)
	@ln -f $</build/core_d.dll $(@:build=luce/core_d.dll)
	@ln -f $</build/intermediate/Release/libluce_win.a $(@:build=luce/libluce.a)
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).win32-5.1.zip luce/core.dll luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).win32-5.1_dbg.zip luce/core_d.dll luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).win32-5.1_static.zip luce/libluce.a luce.lua

$(OUT)/$(VERSION)/luce.$(VERSION).win32-5.1.zip: $(OUT)/$(VERSION)/Win32/build \
											     $(OUT)/$(VERSION)/Win32/luce/core.dll \
											     $(OUT)/$(VERSION)/Win32/luce/core_d.dll \
											     $(OUT)/$(VERSION)/Win32/luce/libluce.a \
											     $(OUT)/$(VERSION)/Win32/luce.lua \
											     $(OUT)/$(VERSION)/luce.$(VERSION).win32-5.1_dbg.zip \
											     $(OUT)/$(VERSION)/luce.$(VERSION).win32-5.1_static.zip

win32: $(OUT)/$(VERSION)/luce.$(VERSION).win32-5.1.zip

$(OUT)/$(VERSION)/Win32-5.2/build: MingW $(LUCE_LIB)
	@echo Building for Win32 5.2
	@mkdir -p $(shell dirname $(@))/luce
	@cp -f $(OUT)/$(VERSION)/luce.lua $(shell dirname $(@))/
	@cd $< && ./wrapper-52 && ./wrapper-52 debug
	@ln -f $</build52/core.dll $(@:build=luce/core.dll)
	@ln -f $</build52/core_d.dll $(@:build=luce/core_d.dll)
	@ln -f $</build52/intermediate/Release/libluce_win.a $(@:build=luce/libluce.a)
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).win32-5.2.zip luce/core.dll luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).win32-5.2_dbg.zip luce/core_d.dll luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).win32-5.2_static.zip luce/libluce.a luce.lua

$(OUT)/$(VERSION)/luce.$(VERSION).win32-5.2.zip: $(OUT)/$(VERSION)/Win32-5.2/build \
												 $(OUT)/$(VERSION)/Win32-5.2/luce/core.dll \
												 $(OUT)/$(VERSION)/Win32-5.2/luce/core_d.dll \
												 $(OUT)/$(VERSION)/Win32-5.2/luce/libluce.a \
												 $(OUT)/$(VERSION)/Win32-5.2/luce.lua \
											     $(OUT)/$(VERSION)/luce.$(VERSION).win32-5.2_dbg.zip \
											     $(OUT)/$(VERSION)/luce.$(VERSION).win32-5.2_static.zip

win32-5.2: $(OUT)/$(VERSION)/luce.$(VERSION).win32-5.2.zip

$(OUT)/$(VERSION)/MacOSX64/build: MacOSX-cross $(LUCE_LIB)
	@echo Building for MacOSX64 5.1
	@mkdir -p $(shell dirname $(@))/luce
	@cp -f $(OUT)/$(VERSION)/luce.lua $(shell dirname $(@))/
	@cd $< && ./wrapper && ./wrapper debug
	@ln -f $</build/core.so $(@:build=luce/core.so)
	@ln -f $</build/core_d.so $(@:build=luce/core_d.so)
	@ln -f $</build/intermediate/Release/libluce_osx.a $(@:build=luce/libluce.a)
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).osx64-5.1.zip luce/core.so luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).osx64-5.1_dbg.zip luce/core_d.so luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).osx64-5.1_static.zip luce/libluce.a luce.lua

$(OUT)/$(VERSION)/luce.$(VERSION).osx64-5.1.zip: $(OUT)/$(VERSION)/MacOSX64/build \
											     $(OUT)/$(VERSION)/MacOSX64/luce/core.so \
											     $(OUT)/$(VERSION)/MacOSX64/luce/core_d.so \
											     $(OUT)/$(VERSION)/MacOSX64/luce/libluce.a \
											     $(OUT)/$(VERSION)/MacOSX64/luce.lua \
												 $(OUT)/$(VERSION)/luce.$(VERSION).osx64-5.1_dbg.zip \
												 $(OUT)/$(VERSION)/luce.$(VERSION).osx64-5.1_static.zip

macosx64: $(OUT)/$(VERSION)/luce.$(VERSION).osx64-5.1.zip

$(OUT)/$(VERSION)/MacOSX64-5.2/build: MacOSX-cross $(LUCE_LIB)
	@echo Building for MacOSX64 5.2
	@mkdir -p $(shell dirname $(@))/luce
	@cp -f $(OUT)/$(VERSION)/luce.lua $(shell dirname $(@))/
	@cd $< && ./wrapper-52 && ./wrapper-52 debug
	@ln -f $</build52/core.so $(@:build=luce/core.so)
	@ln -f $</build52/core_d.so $(@:build=luce/core_d.so)
	@ln -f $</build52/intermediate/Release/libluce_osx.a $(@:build=luce/libluce.a)
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).osx64-5.2.zip luce/core.so luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).osx64-5.2_dbg.zip luce/core.so luce.lua
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).osx64-5.2_static.zip luce/libluce.a luce.lua

$(OUT)/$(VERSION)/luce.$(VERSION).osx64-5.2.zip: $(OUT)/$(VERSION)/MacOSX64-5.2/build \
												 $(OUT)/$(VERSION)/MacOSX64-5.2/luce/core.so \
												 $(OUT)/$(VERSION)/MacOSX64-5.2/luce/core_d.so \
												 $(OUT)/$(VERSION)/MacOSX64-5.2/luce/libluce.a \
												 $(OUT)/$(VERSION)/MacOSX64-5.2/luce.lua \
												 $(OUT)/$(VERSION)/luce.$(VERSION).osx64-5.2_dbg.zip \
												 $(OUT)/$(VERSION)/luce.$(VERSION).osx64-5.2_static.zip

macosx64-5.1: $(OUT)/$(VERSION)/luce.$(VERSION).osx64-5.2.zip

$(OUT)/$(VERSION)/iOS6.1/build: iOS
	@echo Building for iOS61
	@mkdir -p $(shell dirname $(@))
	@cd $< && ./wrapper
	@ln -f $</build/intermediate/Release/libluce_ios.a $(@:build=libluce.a)
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).ios61-5.1.zip libluce.a

$(OUT)/$(VERSION)/luce.$(VERSION).ios61-5.1.zip: $(OUT)/$(VERSION)/iOS6.1/build \
											     $(OUT)/$(VERSION)/iOS6.1/libluce.a

ios: $(OUT)/$(VERSION)/luce.$(VERSION).ios61-5.1.zip

$(OUT)/$(VERSION)/Android4.4/build: Android
	@echo Building for Android4.4
	@mkdir -p $(shell dirname $(@))
	@cd $< && ant release
	@ln -f $</libs/armeabi-v7a/libluce_jni.so $(@:build=libluce_jni.so)
	@cd $(shell dirname $(@)) && zip -q -9 ../luce.$(VERSION).android44-5.1.zip libluce_jni.so

$(OUT)/$(VERSION)/luce.$(VERSION).android44-5.1.zip: $(OUT)/$(VERSION)/Android4.4/build \
											         $(OUT)/$(VERSION)/Android4.4/libluce_jni.so

android: $(OUT)/$(VERSION)/luce.$(VERSION).android44-5.1.zip
