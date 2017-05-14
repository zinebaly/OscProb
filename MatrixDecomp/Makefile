
CXX = g++
CXXFLAGS = $(shell root-config --cflags) -fPIC
LDFLAGS = $(shell root-config --glibs)

PACKAGE = $(shell basename $(CURDIR))
HEADERS = $(filter-out $(CURDIR)/LinkDef.h, $(wildcard $(CURDIR)/*.h))
SOURCES = $(wildcard $(CURDIR)/*.cxx)
TARGET_LIB = $(CURDIR)/lib$(PACKAGE).so
DICTIONARY = $(CURDIR)/tmp/dic$(PACKAGE).cxx

all: $(TARGET_LIB)

$(TARGET_LIB): $(DICTIONARY) $(SOURCES)
	@echo "  Building $(PACKAGE)..."
	@g++ -shared -O3 -o$@ $(LDFLAGS) $(CXXFLAGS) -I$(ROOTSYS)/include $^

$(DICTIONARY): $(HEADERS) LinkDef.h
	@mkdir -p tmp
	@rootcint -f $@ -c $^

clean:
	@rm -f $(TARGET_LIB)
	@rm -f $(DICTIONARY)
	@rm -f $(DICTIONARY:%.cxx=%.h)
	@rmdir tmp


.PHONY: clean all