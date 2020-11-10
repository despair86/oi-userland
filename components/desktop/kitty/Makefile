#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2020 Rick V
#

# kitty requires pyton 3.6 or later, our pyton 3.7 is 64-bit exclusive
BUILD_BITS=64
BUILD_STYLE=justmake
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=kitty
COMPONENT_VERSION=0.19.2
COMPONENT_SUMMARY=kitty - the fast, featureful, GPU based terminal emulator
COMPONENT_PROJECT_URL=https://sw.kovidgoyal.net/kitty/
COMPONENT_FMRI=terminal/kitty
COMPONENT_CLASSIFICATION=Applications/System Utilities
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_URL=https://github.com/kovidgoyal/kitty/releases/download/v0.19.2/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=
COMPONENT_LICENSE=GPLv3.0
include $(WS_MAKE_RULES)/common.mk

CFLAGS+= -D_XOPEN_SOURCE=600
CFLAGS+= -D__EXTENSIONS__
CFLAGS+= -Wno-unused-function
CFLAGS+= -Wno-sign-compare

# kitty builds itself all at once
COMPONENT_BUILD_ACTION = true

COMPONENT_INSTALL_ACTION = \
	cd $(@D) ; $(ENV) $(COMPONENT_BUILD_ENV) $(COMPONENT_INSTALL_ENV) \
	$(GMAKE) $(COMPONENT_INSTALL_ARGS) $(COMPONENT_INSTALL_TARGETS)

TEST_TARGET= $(NO_TESTS)

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += image/library/libpng16
REQUIRED_PACKAGES += library/c++/harfbuzz
REQUIRED_PACKAGES += library/lcms2
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += runtime/python-37
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/fontconfig
REQUIRED_PACKAGES += system/library/freetype-2
REQUIRED_PACKAGES += system/library/libdbus
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxkbcommon
