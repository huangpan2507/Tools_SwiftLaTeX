CC=gcc
CXX=g++
DEBUGFLAGS = -g 
CFLAGS = $(DEBUGFLAGS) -DNATIVE_BUILD 
LDFLAGS =  $(DEBUGFLAGS)  
CXX_LINK = $(CXX) -o $@ $(LDFLAGS) 


csources = xetex-io.c xetex-xetex0.c xetex-ini.c xetex-texmfmp.c xetex-errors.c \
xetex-scaledmath.c xetex-output.c xetex-stringpool.c core-memory.c core-bridge.c \
xetex-pagebuilder.c xetex-shipout.c xetex-math.c xetex-ext.c xetex-linebreak.c \
 xetex-pic.c bibtex.c md5.c xetex-wasm.c miniz.c
 
cppsources = teckit-Engine.cpp xetex-XeTeXOTMath.cpp xetex-XeTeXLayoutInterface.cpp \
 xetex-XeTeXFontMgr.cpp xetex-XeTeXFontInst.cpp xetex-XeTeXFontMgr_FC.cpp

graphitesources = graphite2/src/call_machine.cpp \
graphite2/src/gr_char_info.cpp \
graphite2/src/gr_features.cpp \
graphite2/src/gr_face.cpp \
graphite2/src/gr_font.cpp \
graphite2/src/gr_logging.cpp \
graphite2/src/gr_segment.cpp \
graphite2/src/gr_slot.cpp \
graphite2/src/CmapCache.cpp \
graphite2/src/Code.cpp \
graphite2/src/Collider.cpp \
graphite2/src/Decompressor.cpp \
graphite2/src/Face.cpp \
graphite2/src/FeatureMap.cpp \
graphite2/src/Font.cpp \
graphite2/src/GlyphFace.cpp \
graphite2/src/GlyphCache.cpp \
graphite2/src/Intervals.cpp \
graphite2/src/Justifier.cpp \
graphite2/src/NameTable.cpp \
graphite2/src/Pass.cpp \
graphite2/src/Position.cpp \
graphite2/src/Segment.cpp \
graphite2/src/Silf.cpp \
graphite2/src/Slot.cpp \
graphite2/src/Sparse.cpp \
graphite2/src/TtfUtil.cpp \
graphite2/src/UtfCodec.cpp


headers = xetex-XeTeXFontMgr.h xetex-XeTeXLayoutInterface.h xetex-XeTeXOTMath.h xetex-XeTeXFontMgr_FC.h \
			xetex-XeTeXFontInst.h xetex-xetexd.h xetex-web.h xetex-swap.h xetex-stringpool.h xetex-ext.h \
			xetex-core.h xetex-constants.h teckit-Format.h teckit-cxx-Engine.h teckit-Compiler.h teckit-Common.h \
			teckit-c-Engine.h md5.h core-memory.h core-strutils.h core-foundation.h core-bridge.h bibtex.h

cobjects = $(csources:.c=.o)

cppobjects = $(cppsources:.cpp=.o)

graphiteobjects = $(graphitesources:.cpp=.o)

swiftlatex: $(headers) $(cobjects) $(cppobjects) $(graphiteobjects)
	$(CXX_LINK) $(cobjects) $(cppobjects) $(graphiteobjects) -lfreetype -lharfbuzz    -licuuc   -lharfbuzz-icu  -lcurl

$(cobjects): %.o: %.c
	$(CC) -c $(CFLAGS) -I. -I/usr/include/freetype2 -I/usr/include/harfbuzz  $< -o $@

$(cppobjects): %.o: %.cpp
	$(CXX) -c $(CFLAGS) -I. -I/usr/include/freetype2 -I/usr/include/harfbuzz  $< -o $@

$(graphiteobjects): %.o: %.cpp
	$(CXX) -c $(CFLAGS)  -I graphite2/include -I graphite2/src -DGRAPHITE2_NFILEFACE -DGRAPHITE2_NTRACING $< -o $@

clean:
	rm -f *.o graphite2/src/*.o swiftlatex
	
