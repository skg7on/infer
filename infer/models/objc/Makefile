# Copyright (c) 2015 - present Facebook, Inc.
# All rights reserved.
#
# This source code is licensed under the BSD style license found in the
# LICENSE file in the root directory of this source tree. An additional grant
# of patent rights can be found in the PATENTS file in the same directory.

ROOT_DIR = ../../..
include $(ROOT_DIR)/Makefile.config

OBJC_MODELS_FILE = $(SPECS_LIB_DIR)/objc_models
OBJC_MODELS_SOURCES = $(shell find src/ -name "*.m" -or -name "*.c")

INFER = INFER_ANALYZE_MODELS=1 $(BIN_DIR)/infer

all: $(OBJC_MODELS_FILE)

$(OBJC_MODELS_FILE): $(OBJC_MODELS_SOURCES) $(CLANG_DEPS)
# make clean in src/ in case $(CLANG_DEPS) have changed
	$(MAKE) -C src clean
	$(INFER) -o out/ --models_mode --no_failures_allowed -- $(MAKE) -C src
	touch $(OBJC_MODELS_FILE)

install: $(OBJC_MODELS_FILE)
	$(INSTALL) -m 644 -C out/specs/*.specs $(SPECS_LIB_DIR)

clean:
	@rm -f $(OBJC_MODELS_FILE)
	$(MAKE) -C src clean

.PHONY: all clean install
