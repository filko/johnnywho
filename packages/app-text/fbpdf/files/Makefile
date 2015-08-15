all: fbpdf fbdjvu
%.o: %.c doc.h
	$(CC) -c $(CFLAGS) $<
clean:
	-rm -f *.o fbpdf fbdjvu fbpdf2

# pdf support using mupdf
fbpdf: fbpdf.o mupdf.o draw.o
	$(CC) -o $@ $^ $(LDFLAGS) -lmupdf -lmujs -lfreetype \
			-ljbig2dec -ljpeg -lz -lopenjpeg -lm -lcrypto
# djvu support
fbdjvu: fbpdf.o djvulibre.o draw.o
	$(CC) -o $@ $^ $(LDFLAGS) -ldjvulibre -ljpeg -lm -lstdc++ -lpthread

# pdf support using poppler
poppler.o: poppler.c
	$(CXX) -c $(CFLAGS) `$(PKG_CONFIG) --cflags poppler-cpp` $<
fbpdf2: fbpdf.o poppler.o draw.o
	$(CXX) -o $@ $^ $(LDFLAGS) `$(PKG_CONFIG) --libs poppler-cpp`
