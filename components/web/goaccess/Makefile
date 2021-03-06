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
# Copyright 2016 Adam Stevko
#
BUILD_BITS=64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		goaccess
COMPONENT_VERSION=	1.4
COMPONENT_SUMMARY=	GoAccess is an open source real-time web log analyzer and interactive viewer that runs in a terminal in *nix systems or through your browser.
COMPONENT_PROJECT_URL=	https://goaccess.io/
COMPONENT_FMRI=		web/goaccess
COMPONENT_CLASSIFICATION=Web Services/Application and Web Servers
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_URL=	https://tar.goaccess.io/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH= sha256:e8fbb9ff852556d72dfd9f1d0134ba075ce5b4c41289902a6f4e0d97c69377be
COMPONENT_LICENSE=	MIT
COMPONENT_LICENSE_FILE=	$(COMPONENT_NAME).license

include $(WS_MAKE_RULES)/common.mk

COMPONENT_PRE_CONFIGURE_ACTION= \
	$(CLONEY) $(SOURCE_DIR) $(@D)

CONFIGURE_OPTIONS+= --sysconfdir=/etc
CONFIGURE_OPTIONS+= --enable-geoip=legacy

CFLAGS+= -std=gnu99

REQUIRED_PACKAGES += database/geoip
REQUIRED_PACKAGES += library/ncurses
REQUIRED_PACKAGES += system/library
