INSTALLDIR = $(HOME)/pmix-install
INCLUDES = -I. -I../../test -I../../include -I../.. -I../../src/include
vpath %.h .:../../test:../../include:../..:../../src/include
LDIR = $(INSTALLDIR)/lib

CC = gcc
CFLAGS = $(INCLUDES) -Wfatal-errors #-Wall -Wextra -Wpedantic -Wconversion -Wshadow
LDFLAGS = -Wl,-rpath,$(LDIR)
LIBS =-lpmix -lpthread -levent

# Executables
EXE = pmix_test test_init_fin

# List of all .c source files.
PCFILES = pmix_test.c test_common.c cli_stages.c utils.c test_server.c server_callbacks.c
TCFILES = test_init_fin.c test_common.c
CFILES = $(PCFILES) $(TCFILES)

OBJ = $(CFILES:%.c=%.o)
POBJ = $(PCFILES:%.c=%.o)
TOBJ = $(TCFILES:%.c=%.o)

all: pmix_test test_init_fin
.PHONY: all

clean:
	rm -f $(EXE) $(OBJ) $(DEP)
.PHONY: clean

pmix_test: $(POBJ) 
	$(CC) -o $@ $^ $(CFLAGS) -L$(LDIR) $(LDFLAGS) $(LIBS)

test_init_fin: $(TOBJ)
	$(CC) -o $@ $^ $(CFLAGS) -L$(LDIR) $(LDFLAGS) $(LIBS)

%.o : %.c
	$(CC) -c -o $@ $< $(CFLAGS)

