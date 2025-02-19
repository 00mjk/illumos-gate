#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
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
# Copyright 2008 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#
#

include		../Makefile.com
include		../../Makefile.tools
include		$(SGSHOME)/libld/Makefile.com

.KEEP_STATE:

#
# By using libld's Makefile.com LDLIBS ends up pointing to the proto
# area and many of the directories of cmd/sgs. As such, we need to reset
# that and just make sure to find everything relative to the tools proto
# area.
#
LDLIBS =
CW_LINKER =

CPPFLAGS = $(NATIVE_CPPFLAGS) -DUSE_LIBLD_MALLOC -I$(SRC)/lib/libc/inc \
		    -I$(SRC)/uts/common/krtld -I$(SRC)/uts/sparc \
		    -I$(SRC)/uts/common
LDLIBS +=	-L../libconv -lconv -L$(ROOTONBLDLIBMACH) -llddbg -lelf -lc
NATIVE_LIBS +=	libc.so

DYNFLAGS +=	$(VERSREF) '-R$$ORIGIN'
CFLAGS = $(NATIVE_CFLAGS)

all:		$(DYNLIB) $(LIBLINKS)

install:	all $(ROOTONBLDLIBMACH)/$(DYNLIB) $(ROOTONBLDLIBMACH)/$(LIBLINKS)

$(ROOTONBLDLIBMACH)/$(DYNLIB): $(PICS) $(ROOTONBLDLIBMACH)
		$(BUILD.SO)
		$(POST_PROCESS_SO)

$(ROOTONBLDLIBMACH)/$(LIBLINKS): $(ROOTONBLDLIBMACH)/$(DYNLIB)
		@$(RM) $(ROOTONBLDLIBMACH)/$(LIBLINKS)
		$(SYMLINK) $(DYNLIB) $(ROOTONBLDLIBMACH)/$(LIBLINKS)

include		$(SGSHOME)/libld/Makefile.targ
