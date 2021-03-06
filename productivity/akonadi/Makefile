# $OpenBSD: Makefile,v 1.3 2010/11/22 08:37:02 espie Exp $

CATEGORIES =	productivity
COMMENT =	PIM cache and access services
DISTNAME =	akonadi-${AKONADI_VERSION}
REVISION =	1

SHARED_LIBS = 	akonadiprotocolinternals 1.0	# 1.0

EXTRACT_SUFX =	.tar.bz2
MASTER_SITES =	${MASTER_SITE_KDE:=stable/akonadi/src/}

WANTLIB =  c m pthread stdc++
WANTLIB += lib/qt4/QtDBus lib/qt4/QtGui lib/qt4/QtNetwork
WANTLIB += lib/qt4/QtSql lib/qt4/QtXml
WANTLIB += boost_program_options-mt sqlite3 soprano

# LGPLv2+
PERMIT_DISTFILES_CDROM =        Yes
PERMIT_DISTFILES_FTP =          Yes
PERMIT_PACKAGE_CDROM =          Yes
PERMIT_PACKAGE_FTP =            Yes

MODULES =		x11/kde4
MODKDE4_USE =

BUILD_DEPENDS =		databases/mysql,-server \
			x11/qt4 \
			x11/qt4,-mysql

# Build PostgreSQL support for those who want it
BUILD_DEPENDS +=	x11/qt4,-postgresql

RUN_DEPENDS =		misc/shared-mime-info

# Do not force PostgreSQL as a dependency, MySQL is most tested one.
RUN_DEPENDS +=		databases/mysql,-server \
			x11/qt4,-mysql

LIB_DEPENDS =		STEM->=${SOPRANO_VERSION}:databases/soprano \
			devel/boost

CONFIGURE_ARGS =	-DDATABASE_BACKEND:String=MYSQL

.include <bsd.port.mk>
