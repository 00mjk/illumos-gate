#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License, Version 1.0 only
# (the "License").  You may not use this file except in compliance
# with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
#
# Copyright 2005 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#
# Copyright 2013 Nexenta Systems, Inc.  All rights reserved.
# Copyright 2015 Gary Mills
# Copyright 2019 Peter Tribble.
#

MODULE = libfksmbsrv.so
MDBTGT = proc

MODSRCS = smbsrv.c smbsrv_pcap.c list.c

include ../../../../Makefile.cmd
include ../../Makefile.sparcv7
include ../../../Makefile.module

MODSRCS_DIR = ../../../common/modules/smbsrv
GENUNIX_DIR = ../../../common/modules/genunix

# Note: need our sys includes _before_ ENVCPPFLAGS, proto etc.
CPPFLAGS.first += -I../../../../../lib/smbsrv/libfksmbsrv/common
CPPFLAGS.first += -I../../../../../lib/libfakekernel/common

CPPFLAGS += -I../../../../../uts/common

CSTD=	$(CSTD_GNU99)

dmod/%.o: $(GENUNIX_DIR)/%.c
	$(COMPILE.c) -o $@ $<
	$(CTFCONVERT_O)
