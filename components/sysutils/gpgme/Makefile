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
# Copyright (c) 2011, 2012, Oracle and/or its affiliates. All rights reserved.
#

BUILD_BITS = 32_and_64
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gpgme
COMPONENT_VERSION=	1.13.1
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_PROJECT_URL=	http://www.gnupg.org/related_software/gpgme/
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH=	\
    sha256:c4e30b227682374c23cddc7fdb9324a99694d907e79242a25a4deeedb393be46
COMPONENT_ARCHIVE_URL=	ftp://ftp.gnupg.org/gcrypt/gpgme/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI=	library/security/gpgme
COMPONENT_SUMMARY=	GnuPG Made Easy
COMPONENT_DESCRIPTION=	A library designed to make access to GnuPG easier for applications
COMPONENT_CLASSIFICATION= System/Libraries
COMPONENT_LICENSE=	GPLv2,LGPLv2

include $(WS_MAKE_RULES)/common.mk

COMPONENT_PREP_ACTION = ( cd $(@D) && autoreconf -fi )

PATH = $(PATH.gnu)

CFLAGS += $(CPP_LARGEFILES)
CFLAGS += $(XPG6MODE)
CFLAGS += $(CPP_POSIX)
CFLAGS += $(CPP_C99_EXTENDED_MATH)
CFLAGS += $(gcc_C99_ENABLE)

CONFIGURE_ENV +=	CFLAGS="$(CFLAGS)"
CONFIGURE_ENV +=	INSTALL="$(INSTALL)"

CONFIGURE_OPTIONS  +=		--localstatedir=/var
CONFIGURE_OPTIONS  +=		--infodir=$(CONFIGURE_INFODIR)
CONFIGURE_OPTIONS  +=		--enable-shared
CONFIGURE_OPTIONS  +=		--disable-static
CONFIGURE_OPTIONS  +=		--with-gpg-error-prefix=$(CONFIGURE_PREFIX)
CONFIGURE_OPTIONS  +=		--enable-largefile
CONFIGURE_OPTIONS  +=		--with-pth=$(CONFIGURE_PREFIX)
CONFIGURE_OPTIONS  +=		--enable-languages="cl"
CONFIGURE_OPTIONS  +=		--enable-gpg-test
CONFIGURE_OPTIONS  +=		--enable-gpgsm-test
CONFIGURE_OPTIONS  +=		--enable-gpgconf-test
CONFIGURE_OPTIONS  +=		--with-gpg=$(USRBINDIR)/gpg2
CONFIGURE_OPTIONS  +=		--with-gpgsm=$(USRBINDIR)/gpgsm
CONFIGURE_OPTIONS  +=		--with-gpgconf=$(USRBINDIR)/gpgconf
CONFIGURE_OPTIONS  +=		--with-pic

# Please see comments in patches/GNUPGHOME.patch
GNUPG_HOME_DIR = GNUPGHOME
GNUPG_HOME_LINK = LINK
COMPONENT_PRE_BUILD_ACTION += ( \
    set -x; \
    DEST="$(@D)/$(GNUPG_HOME_DIR)"; \
    LINK="$$(mktemp)"; \
    echo "$$LINK" | tee "$(@D)/$(GNUPG_HOME_LINK)"; \
    $(RM) "$$DEST" "$$LINK"; \
    $(MKDIR) "$$DEST"; \
    ln -s "$$DEST" "$$LINK"; \
);

COMPONENT_POST_BUILD_ACTION += ( \
    set -x; \
    LINK="$$(< "$(@D)/$(GNUPG_HOME_LINK)")"; \
    [ -z "$$LINK" ] || $(RM) "$$LINK"; \
);

COMPONENT_BUILD_ARGS += GNUPGHOME="$$(< "$(@D)/$(GNUPG_HOME_LINK)")"

COMPONENT_PRE_TEST_ACTION = $(COMPONENT_PRE_BUILD_ACTION)
COMPONENT_POST_TEST_ACTION = $(COMPONENT_POST_BUILD_ACTION)
COMPONENT_TEST_ARGS += GNUPGHOME="$$(< "$(@D)/$(GNUPG_HOME_LINK)")"

REQUIRED_PACKAGES += library/security/libassuan
REQUIRED_PACKAGES += library/security/libgpg-error
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
