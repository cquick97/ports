# Created by: Franco Fichtner <franco@opnsense.org>
# $FreeBSD$

PORTNAME=	libreswan
PORTVERSION=	3.21
DISTVERSIONPREFIX=v
CATEGORIES=	security

MAINTAINER=	franco@opnsense.org
COMMENT=	Libreswan IPsec implementation

LICENSE=	GPLv2

BUILD_DEPENDS=	bash:shells/bash
LIB_DEPENDS=	libnss3.so:security/nss
RUN_DEPENDS=	bash:shells/bash

USE_GITHUB=	yes

ALL_TARGET=	base

MAKE_ENV=	BUILDENV=freebsd OSDEP=bsd

USE_HARDENING=	pie:off relro:off

MAKE_ENV=	WERROR_CFLAGS=

USES=		bison gmake pkgconfig

MAKE_JOBS_UNSAFE=yes

PLIST_FILES=	%%TODO%%

post-patch:
	${REINPLACE_CMD} -e 's|/bin/bash|${LOCALBASE}/bin/bash|g' \
	    ${WRKSRC}/mk/config.mk
	${REINPLACE_CMD} -e 's|- timezone||g' \
	    ${WRKSRC}/lib/libswan/asn1.c
	${REINPLACE_CMD} -e 's|.include..linux.version.h.||g' \
	    ${WRKSRC}/linux/include/libreswan/pfkey.h
	${REINPLACE_CMD} -e 's|KERNEL_VERSION..,..,...|0|g' \
	    ${WRKSRC}/linux/include/libreswan/pfkey.h
	${REINPLACE_CMD} -e 's|truncate(|truncatex(|g' \
	    ${WRKSRC}/lib/libswan/lswlog.c
	${REINPLACE_CMD} -e 's|netkey/key_var\.h|netipsec/key_var.h|g' \
	    ${WRKSRC}/lib/libbsdpfkey/pfkey.c
	${REINPLACE_CMD} -e 's|netinet6/ipsec\.h|netipsec/ipsec.h|g' \
	    ${WRKSRC}/lib/libbsdpfkey/pfkey.c
	${REINPLACE_CMD} -e 's|^		int so;$$|		int so,|g' -e 's|reqid_t reqid;$$|reqid_t reqid,|g' \
	    -e 's| keymat;$$| keymat,|g' -e 's| l_alloc;$$| l_alloc,|g' \
	    ${WRKSRC}/lib/libbsdpfkey/pfkey.c
	${REINPLACE_CMD} -e 's|netinet6/ipsec\.h|netipsec/ipsec.h|g' \
	    ${WRKSRC}/lib/libbsdpfkey/pfkey_dump.c
	${REINPLACE_CMD} -e 's|netkey/key_var\.h|netipsec/key_var.h|g' \
	    ${WRKSRC}/lib/libbsdpfkey/pfkey_dump.c
	${REINPLACE_CMD} -e 's|netkey/key_debug\.h|netipsec/key_debug.h|g' \
	    ${WRKSRC}/lib/libbsdpfkey/pfkey_dump.c

.include <bsd.port.mk>
