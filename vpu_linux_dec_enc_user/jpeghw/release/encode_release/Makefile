#!/bin/bash

# Makefile using libtool for vpu common library.

TOP_DIR = $(shell pwd)

# define compiler
#TOOLCHAIN ?= /user/bin
#export CROSS_COMPILER := arm-linux-gnueabihf-
#TOOLCHAIN ?= ../../../toolschain/4.4.3/bin/
export CROSS_COMPILER := 
CC     := $(CROSS_COMPILER)gcc
CXX    := $(CROSS_COMPILER)g++
AR     := $(CROSS_COMPILER)ar
AS     := $(CROSS_COMPILER)as
LD     := $(CROSS_COMPILER)ld
RANLIB := $(CROSS_COMPILER)ranlib
STRIP  := $(CROSS_COMPILER)strip

# define the source code
#SRC_CODE_C = $(wildcard *.c)
#SRC_CODE_CPP = $(wildcard *.cpp)

SRC_CODE_C = \
                hw_jpegenc.c

SRC_CODE_CPP = 

#INCLUDE = -I. -I$(TOP_DIR) -I$(TOP_DIR)/include
INCLUDE = -I. -I$(TOP_DIR) -I$(TOP_DIR)/../../src_enc/inc -I$(TOP_DIR)/../../src_enc \
	-I$(TOP_DIR)/../../src_enc/common -I$(TOP_DIR)/../../src_enc/jpeg \
	-I$(TOP_DIR)/../../../libvpu/common/include -I$(TOP_DIR)/../../../libvpu/common

# define generation

OBJ_C = $(SRC_CODE_C:.c=.o)
OBJ_CPP = $(SRC_CODE_CPP:.cpp=.o)

LIB_NAME = libjpeghwenc.so

# define the build flag
CFLAGS += $(INCLUDE)
#CFLAGS += -fPIC
#LDFLAGS    

SHARED_LIB += -L$(TOP_DIR)/../../../sharelib/
SHARED_LIB += -lvpu -lon2jpegenc -lOn2enc_common

#RUN_LIB_DIR = -rpath $(TOP_DIR)/../../../sharelib/libvpu.so $(TOP_DIR)/../../../sharelib/libion.so
#RUN_LIB_DIR = -rpath $(TOP_DIR)/../../../sharelib/libvpu.so 
RUN_LIB_DIR = 

# build steps

.PHONY : all all_src install clean

all : $(OBJ_C) $(OBJ_CPP)
#	$(CC) $(CFLAGS) $^ -shared -fPIC -o $(LIB_NAME)
	$(CC) $(CFLAGS) $(SRC_CODE_C)  $(SRC_CODE_CPP) $(SHARED_LIB) -shared -fPIC -o $(LIB_NAME) $(RUN_LIB_DIR)

$(OBJ_C) : %.o : %.c
	$(CC) $(CFLAGS) -c $< -o $@

$(OBJ_CPP) : %.o : %.cpp
	$(CXX) $(CFLAGS) -c $< -o $@

#all_src :
#$(OBJ_CPP) : %.o : %.cpp
#	$(CXX) $(CFLAGS) -c $< -o $@

clean :
	@rm -rf $(OBJ_C) $(OBJ_CPP) $(LIB_NAME)

install : all
	@echo "cp "$(LIB_NAME)" to sharelib"
	@cp $(LIB_NAME) ../../../sharelib/
