# $OpenBSD$

CATEGORIES =	devel x11
COMMENT =	integrated development environment for KDE 4
DISTNAME =	kdevelop-${KDEVELOP_VERSION}
HOMEPAGE =	http://www.kdevelop.org/

EXTRACT_SUFX =	.tar.bz2

SHARED_LIBS =	kdev4cmakecommon	0.0
SHARED_LIBS +=	kdev4cppduchain		0.0
SHARED_LIBS +=	kdev4cppparser		0.0
SHARED_LIBS +=	kdev4cpprpp		0.0

MASTER_SITES =	${MASTER_SITE_KDE:=stable/kdevelop/${KDEVELOP_VERSION}/src/}
DIST_SUBDIR =	kde

# GPLv2+, LGPLv2.1+, GNU FDLv1.2
PERMIT_DISTFILES_CDROM =        Yes
PERMIT_DISTFILES_FTP =          Yes
PERMIT_PACKAGE_CDROM =          Yes
PERMIT_PACKAGE_FTP =            Yes

WANTLIB =  c m pthread stdc++
WANTLIB += lib/qt4/QtDBus lib/qt4/QtDeclarative lib/qt4/QtGui
WANTLIB += lib/qt4/QtHelp lib/qt4/QtNetwork lib/qt4/QtScript
WANTLIB += lib/qt4/QtSvg lib/qt4/QtWebKit lib/qt4/QtXml
WANTLIB += kcmutils kdeclarative kdeui
WANTLIB += kdevplatformdebugger kdevplatformdocumentation
WANTLIB += kdevplatforminterfaces kdevplatformlanguage
WANTLIB += kdevplatformoutputview kdevplatformproject kdevplatformshell
WANTLIB += kdevplatformutil kdevplatformvcs kemoticons kidletime kio
WANTLIB += knewstuff3 knotifyconfig kparts kprintutils ktexteditor kutils
WANTLIB += nepomuk nepomukutils plasma
WANTLIB += processcore processui
WANTLIB += soprano sublime threadweaver
WANTLIB += kasten2controllers kasten2core kasten2gui
WANTLIB += kasten2okteta1controllers kasten2okteta1core
WANTLIB += kasten2okteta1gui okteta1core okteta1gui

MODULES =	x11/kde4
MODKDE4_USE =	workspace

# Uses files with "{...}" in names
USE_GMAKE =	Yes

BUILD_DEPENDS =	misc/shared-mime-info

LIB_DEPENDS = 	STEM->=${KDEVPLATFORM_VERSION}:devel/kdevplatform \
		x11/kde4/sdk

.include <bsd.port.mk>
