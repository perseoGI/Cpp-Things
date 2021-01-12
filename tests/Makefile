CFLAGS			:= -Wall
BIND			:= bin

ifeq ($(OS),Windows_NT)
	CC := x86_64-w64-mingw32-gcc
	# TODO
else
	CC := g++
	UNAME_S := $(shell uname -s)
    ifeq ($(UNAME_S),Linux)
		# Compiling for Linux

		# Libs for every distro except useless Ubuntu...
		ifeq ($(shell grep Ubuntu /etc/os-release), )
			LIBS_I := `pkg-config --libs-only-l gtest gmock`
		else
		# Libs for Ubuntu
			LIBS_I := -lgtest -pthread /usr/local/lib/libgtest.a
		endif

    endif
    ifeq ($(UNAME_S),Darwin)
		# Compiling for Mac OS
		# TODO
	endif
endif



all: prepare googletest gtest test

prepare:
	mkdir -p $(BIND)

googletest:
	$(CC) $(CFLAGS) -c gtest-test.C -o $(BIND)/gtest-test.o

gtest:
	$(CC) $(CFLAGS) $(BIND)/gtest-test.o $(LIBS_I) -o $(BIND)/gtest-test

test:
	./$(BIND)/gtest-test

clean:
	rm -rf $(BIND)
