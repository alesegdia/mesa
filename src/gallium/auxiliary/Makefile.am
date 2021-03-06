if HAVE_LOADER_GALLIUM
SUBDIRS := pipe-loader
endif

include Makefile.sources
include $(top_srcdir)/src/gallium/Automake.inc

noinst_LTLIBRARIES = libgallium.la

AM_CFLAGS = \
	-I$(top_srcdir)/src/loader \
	-I$(top_builddir)/src/glsl/nir \
	-I$(top_srcdir)/src/gallium/auxiliary/util \
	$(GALLIUM_CFLAGS) \
	$(VISIBILITY_CFLAGS) \
	$(MSVC2008_COMPAT_CXXFLAGS)

AM_CXXFLAGS = \
	$(VISIBILITY_CXXFLAGS) \
	$(MSVC2008_COMPAT_CXXFLAGS)

libgallium_la_SOURCES = \
	$(C_SOURCES) \
	$(NIR_SOURCES) \
	$(GENERATED_SOURCES)

if HAVE_MESA_LLVM

AM_CFLAGS += \
	$(LLVM_CFLAGS)

AM_CXXFLAGS += \
	$(GALLIUM_CFLAGS) \
	$(LLVM_CXXFLAGS)

libgallium_la_SOURCES += \
	$(GALLIVM_SOURCES)

endif

indices/u_indices_gen.c: $(srcdir)/indices/u_indices_gen.py
	$(AM_V_at)$(MKDIR_P) indices
	$(AM_V_GEN) $(PYTHON2) $< > $@

indices/u_unfilled_gen.c: $(srcdir)/indices/u_unfilled_gen.py
	$(AM_V_at)$(MKDIR_P) indices
	$(AM_V_GEN) $(PYTHON2) $< > $@

util/u_format_table.c: $(srcdir)/util/u_format_table.py $(srcdir)/util/u_format_pack.py $(srcdir)/util/u_format_parse.py $(srcdir)/util/u_format.csv
	$(AM_V_at)$(MKDIR_P) util
	$(AM_V_GEN) $(PYTHON2) $(srcdir)/util/u_format_table.py $(srcdir)/util/u_format.csv > $@


noinst_LTLIBRARIES += libgalliumvl_stub.la
libgalliumvl_stub_la_SOURCES = \
	$(VL_STUB_SOURCES)

if NEED_GALLIUM_VL

COMMON_VL_CFLAGS = \
	$(AM_CFLAGS) \
	$(VL_CFLAGS) \
	$(DRI2PROTO_CFLAGS) \
	$(LIBDRM_CFLAGS) \
	$(GALLIUM_PIPE_LOADER_DEFINES) \
	-DPIPE_SEARCH_DIR=\"$(libdir)/gallium-pipe\"

if HAVE_GALLIUM_STATIC_TARGETS
COMMON_VL_CFLAGS += \
	-DGALLIUM_STATIC_TARGETS=1

endif # HAVE_GALLIUM_STATIC_TARGETS

noinst_LTLIBRARIES += libgalliumvl.la

libgalliumvl_la_CFLAGS = \
	$(COMMON_VL_CFLAGS)

libgalliumvl_la_SOURCES = \
	$(VL_SOURCES)

if NEED_GALLIUM_VL_WINSYS

noinst_LTLIBRARIES += libgalliumvlwinsys.la

libgalliumvlwinsys_la_CFLAGS = \
	$(COMMON_VL_CFLAGS)

libgalliumvlwinsys_la_SOURCES = \
	$(VL_WINSYS_SOURCES)

endif

endif

EXTRA_DIST = \
	SConscript \
	indices/u_indices.c \
	indices/u_unfilled_indices.c \
	indices/u_indices_gen.py \
	indices/u_unfilled_gen.py \
	postprocess/ADDING \
	rbug/README \
	target-helpers \
	util/u_format.csv \
	util/u_format_pack.py \
	util/u_format_parse.py \
	util/u_format_table.py
