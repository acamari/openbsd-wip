# $OpenBSD: Makefile,v 1.55 2012/07/04 12:49:20 ajacoutot Exp $

# XXX Don't even think of updating ocaml alone.
# Do check that the ports that depend on it still work, or repair them.

NOT_FOR_ARCHS=	hppa

BROKEN-powerpc=	'struct sigcontext' has no member named 'regs'

COMMENT-main =	ML language based on complete class-based objective system
COMMENT-run =	runtime system for OCaml bytecode executables

VERSION=4.00.1

DISTNAME =	ocaml-${VERSION}

MULTI_PACKAGES = -main -run
PKGNAME-main =	ocaml-${VERSION}
PKGNAME-run =	ocaml-run-${VERSION}
# OCaml has no binary compatibility between releases.
PKGSPEC-main =	ocaml-=${VERSION}
PKGSPEC-run =	ocaml-run-=${VERSION}

CATEGORIES=	lang
BASENAME =	${DISTNAME:C/\.[^.]*$//}
MASTER_SITES=	http://caml.inria.fr/pub/distrib/${BASENAME}/
DOCFILES=	${BASENAME}-refman-html.tar.gz
DISTFILES=	${DISTNAME}.tar.gz ${DOCFILES}

HOMEPAGE=	http://www.ocaml.org/
MAINTAINER=	Anil Madhavapeddy <avsm@openbsd.org>

# QPL/LGPL
PERMIT_PACKAGE_CDROM=	Yes
PERMIT_PACKAGE_FTP=	Yes
PERMIT_DISTFILES_CDROM=	Yes
PERMIT_DISTFILES_FTP=	Yes

MODULES+= lang/tcl x11/tk

VMEM_WARNING=	Yes
CONFIGURE_STYLE=	simple
CONFIGURE_ARGS+=-tkdefs '-I${MODTCL_INCDIR} -I${MODTK_INCDIR}'
CONFIGURE_ARGS+=-tklibs -L${LOCALBASE}/lib
CONFIGURE_ARGS+=-prefix ${PREFIX}
CONFIGURE_ARGS+=-cc '${CC} ${CFLAGS}'
CONFIGURE_ARGS+=-x11include ${X11BASE}/include -x11lib ${X11BASE}/lib
CONFIGURE_ENV+=OPENBSD_LOCALBASE="${LOCALBASE}"

# ocaml's configure script is too smart for its own good
FAKE_FLAGS=	PREFIX=${WRKINST}${PREFIX}

USE_GMAKE=	Yes

# Don't append, but override defaults from ocaml.port.mk inclusion above!
BUILD_DEPENDS =		${MODTK_BUILD_DEPENDS} \
			devel/gdb
RUN_DEPENDS =		${MODTK_RUN_DEPENDS}
RUN_DEPENDS-main = 	${RUN_DEPENDS} ${BASE_PKGPATH},-run
LIB_DEPENDS =		${MODTK_LIB_DEPENDS}
WANTLIB =		X11 c curses iberty m pthread z ${MODTK_WANTLIB}

.include <bsd.port.arch.mk>

.if ${PROPERTIES:Mocaml_native}
ALL_TARGET=	world bootstrap opt opt.opt
PKG_ARGS +=	-Dnative=1
.if ${PROPERTIES:Mocaml_native_dynlink}
PKG_ARGS +=	-Ddynlink=1
.else
PKG_ARGS +=	-Ddynlink=0
.endif
.else
ALL_TARGET=	world bootstrap
PKG_ARGS +=	-Dnative=0
.endif

# XXX regress tests only work on archs with native-code compiler
REGRESS_DEPENDS+=	${BUILD_PKGPATH}

post-extract:
	@cp ${WRKSRC}/asmrun/power-elf.S ${WRKSRC}/asmrun/power-bsd.S

post-install:
.if ${PROPERTIES:Mocaml_native}
	@ln -sf ${LOCALBASE}/bin/ocamlbuild.native ${PREFIX}/bin/ocamlbuild
.else
	@ln -sf ${LOCALBASE}/bin/ocamlbuild.byte ${PREFIX}/bin/ocamlbuild
.endif
	@${INSTALL_DATA_DIR} ${PREFIX}/share/doc/ocaml/html/libref
	@${INSTALL_DATA} ${WRKDIR}/htmlman/*.{html,gif} \
		${PREFIX}/share/doc/ocaml/html
	@${INSTALL_DATA} ${WRKDIR}/htmlman/libref/* \
		${PREFIX}/share/doc/ocaml/html/libref
	@strip ${PREFIX}/bin/ocamlrun ${PREFIX}/bin/ocamlyacc
	@${INSTALL_DATA} \
		${WRKSRC}/{LICENSE,Changes} \
		${PREFIX}/share/doc/ocaml

# PFRAG.native was generated from PLIST with:
# egrep '(ocamlopt|\.cmx|\.cmxa|\.cmxs|\.opt|opt\.1|opt.cmi|\.native|\.o)$'

# XXX one test in the suite (testsocket.ml) requires an active
# connection to internet
do-regress:
	@cd ${WRKSRC}/testsuite && ulimit -Sn 256 && ${MAKE_PROGRAM} all

.include <bsd.port.mk>
