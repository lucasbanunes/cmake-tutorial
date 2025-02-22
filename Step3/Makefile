SHELL := /bin/bash

all: build

build:
	mkdir -p build
	cd build && cmake .. && make && cd ..

new_build:
	rm -rf build
	mkdir -p build
	cd build && cmake .. && make && cd ..