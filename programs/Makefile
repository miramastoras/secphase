CC=gcc
INC=-I /home/apps/sonLib/C/inc/ -I /usr/local/include/htslib -I submodules/cigar_it -I submodules/common
STATIC_LIBS=/home/apps/sonLib/lib/sonLib.a
CCFLAGS=$(STATIC_LIBS) $(INC) -lm -lhts -lpthread
BIN_DIR=bin
SRC_DIR=src
MDL_DIR=submodules

MDLS=$(wildcard ${MDL_DIR}/*)
OBJS=$(join $(MDLS), $(MDLS:${MDL_DIR}/%=/%.o))
SRCS=$(wildcard ${SRC_DIR}/*.c)
BINS=$(patsubst ${SRC_DIR}/%.c,${BIN_DIR}/%,$(SRCS))

.PHONY: all

all: ${OBJS} ${BIN_DIR} $(BINS) ${BIN_DIR}/secphase_debug

bin/%: src/%.c $(OBJS)
	$(CC) -o $@ $< $(OBJS) $(CCFLAGS)

bin/secphase_debug: src/secphase.c $(OBJS)
	$(CC) -o$@ $< $(OBJS) -DDEBUG $(CCFLAGS)

${BIN_DIR}:
	@mkdir -p bin

%.o: %.c %.h
	$(CC) -c -o$@ $< $(CCFLAGS)
