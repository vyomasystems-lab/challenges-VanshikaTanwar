# See LICENSE.vyoma for details

TOPLEVEL_LANG ?= verilog

PWD=$(shell pwd)

VERILOG_SOURCES = $(PWD)/dvsd_cmp.v               # provide your design path

TOPLEVEL :=   dvsd_cmp        # design file
MODULE   :=   test_dvsd_cmp  # test file

include $(shell cocotb-config --makefiles)/Makefile.sim

clean_all: clean
	rm -rf *.xml sim_build _pycache_
