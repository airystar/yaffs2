# Makefile for YAFFS direct test
#
#
# YAFFS: Yet another Flash File System. A NAND-flash specific file system.
#
# Copyright (C) 2003-2010 Aleph One Ltd.
#
#
# Created by Charles Manning <charles@aleph1.co.uk>
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License version 2 as
# published by the Free Software Foundation.
#
# NB Warning this Makefile does not include header dependencies.
#
# $Id: Makefile,v 1.24 2010-02-17 02:18:57 charles Exp $

#EXTRA_COMPILE_FLAGS = -DYAFFS_IGNORE_TAGS_ECC

CFLAGS =      -DCONFIG_YAFFS_DIRECT -DCONFIG_YAFFS_YAFFS2 -D CONFIG_YAFFS_DEFINES_TYPES
CFLAGS +=     -DCONFIG_YAFFS_PROVIDE_DEFS -DCONFIG_YAFFSFS_PROVIDE_VALUES -DNO_Y_INLINE
CFLAGS +=    -Wall -g $(EXTRA_COMPILE_FLAGS) -Werror=strict-aliasing 
#CFLAGS +=    -fno-strict-aliasing
CFLAGS +=    -O0
#CFLAGS +=    -DVALGRIND_TEST
#CFLAGS +=     -DCONFIG_YAFFS_CASE_INSENSITIVE

CFLAGS+=   -Wshadow -Werror=pointer-arith -Werror=write-strings
CFLAGS+=   -Werror=strict-prototypes -Werror=missing-parameter-type
CFLAGS+=   -Werror=redundant-decls -Werror=nested-externs -Winline
CFLAGS+=   -Werror=undef

CFLAGS+=   -DCONFIG_YAFFS_USE_PTHREADS -lpthread


COMMONTESTOBJS = yaffscfg2k.o yaffs_osglue.o yaffs_hweight.o \
		 yaffs_ecc.o yaffs_fileem.o yaffs_fileem2k.o yaffsfs.o yaffs_guts.o \
		 yaffs_packedtags1.o yaffs_ramdisk.o yaffs_ramem2k.o \
		 yaffs_tagscompat.o yaffs_packedtags2.o yaffs_nand.o \
		 yaffs_checkptrw.o  yaffs_qsort.o\
		 yaffs_nameval.o yaffs_attribs.o \
		 yaffs_norif1.o  ynorsim.o \
		 yaffs_allocator.o \
		 yaffs_bitmap.o \
		 yaffs_yaffs1.o \
		 yaffs_yaffs2.o \
		 yaffs_verify.o \
		 yaffs_summary.o

#		 yaffs_checkptrwtest.o\


YAFFSDIRECTSYMLINKS = \
          yaffs_ecc.c yaffs_ecc.h yaffs_guts.c yaffs_guts.h \
          yaffs_tagscompat.c yaffs_tagscompat.h \
          yaffs_packedtags1.c yaffs_packedtags1.h yaffs_packedtags2.c yaffs_packedtags2.h \
          yaffs_nand.c yaffs_nand.h yaffs_getblockinfo.h \
          yaffs_checkptrw.h yaffs_checkptrw.c \
          yaffs_nameval.c yaffs_nameval.h \
          yaffs_trace.h yaffs_attribs.h \
          yaffs_allocator.c yaffs_allocator.h \
          yaffs_yaffs1.c yaffs_yaffs1.h \
          yaffs_yaffs2.c yaffs_yaffs2.h \
          yaffs_bitmap.c yaffs_bitmap.h \
          yaffs_verify.c yaffs_verify.h \
          yaffs_summary.c yaffs_summary.h \
	  yaffsfs.c yaffs_flashif.h yaffs_flashif2.h\
          yaffsfs.h yaffs_osglue.h ydirectenv.h \
          yaffscfg.h yaffs_list.h \
          yaffs_qsort.c yportenv.h yaffs_attribs.c \
          yaffs_nandif.c yaffs_nandif.h yaffs_nandemul2k.h \
          yaffs_hweight.h yaffs_hweight.c \



DIRECTTESTOBJS = $(COMMONTESTOBJS) dtest.o

BOOTTESTOBJS = bootldtst.o yboot.o yaffs_fileem.o nand_ecc.o

ALLOBJS = $(sort $(DIRECTTESTOBJS) $(YAFFSTESTOBJS))

TARGETS = directtest2k

all: $(TARGETS)

$(ALLOBJS): %.o: %.c
	gcc -c $(CFLAGS) -o $@ $<


$(YAFFSDIRECTSYMLINKS):
	ln -s ../$@ $@


directtest2k: $(YAFFSDIRECTSYMLINKS) $(DIRECTTESTOBJS)
	gcc -o $@ $(DIRECTTESTOBJS)

yaffs_test: $(YAFFSDIRECTSYMLINKS) $(YAFFSTESTOBJS)
	gcc -o $@ $(YAFFSTESTOBJS)


boottest: $(YAFFSDIRECTSYMLINKS) $(BOOTTESTOBJS)
	gcc -o $@ $(BOOTTESTOBJS)


clean:
	rm -f $(TARGETS) $(ALLOBJS) core $(YAFFSDIRECTSYMLINKS)
