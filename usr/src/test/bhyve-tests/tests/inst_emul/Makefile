#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

# Copyright 2022 Oxide Computer Company

include $(SRC)/cmd/Makefile.cmd
include $(SRC)/cmd/Makefile.cmd.64
include $(SRC)/test/Makefile.com

PROG =	rdmsr \
	wrmsr \
	triple_fault

PAYLOADS = $(PROG)
include ../Makefile.in_guest

COMMON_OBJS =	in_guest.o

CLEANFILES =	$(COMMON_OBJS) $(PAYLOAD_CLEANFILES)
CLOBBERFILES =	$(PROG)

ROOTOPTPKG = $(ROOT)/opt/bhyve-tests
TESTDIR = $(ROOTOPTPKG)/tests/inst_emul

CMDS = $(PROG:%=$(TESTDIR)/%)
$(CMDS) := FILEMODE = 0555

CSTD=		$(CSTD_GNU99)
CPPFLAGS =	-I$(COMPAT)/bhyve -I$(CONTRIB)/bhyve \
		-I$(COMPAT)/bhyve/amd64 -I$(CONTRIB)/bhyve/amd64 \
		$(CPPFLAGS.master) \
		-I$(SRC)/uts/intel/io/vmm \
		-I$(SRC)/uts/intel \
		-I../common

ASFLAGS += -P -D__STDC__ -D_ASM


CFLAGS = -m64
$(PROG) :=	LDLIBS += -lvmmapi

all: $(PROG)

install: all $(CMDS)

clean:
	-$(RM) $(CLEANFILES)
clobber: clean
	-$(RM) $(CLOBBERFILES)

$(CMDS): $(TESTDIR) $(PROG)

$(TESTDIR):
	$(INS.dir)

$(TESTDIR)/%: %
	$(INS.file)

%: %.c pobj_%.o $(COMMON_OBJS)
	$(LINK.c) -o $@ $^ $(LDLIBS)
	$(POST_PROCESS)

%: %.o
	$(LINK.c) -o $@ $^ $(LDLIBS)
	$(POST_PROCESS)
