include ../../Makefile.conf

TARGET_DIR ?= /usr/local/texlive/proposal

all: macros prop

.PHONY: all

macros: macros_download macros_install

.PHONY: macros

prop: prop_download prop_install

.PHONY: prop

clean: macros_clean prop_clean

.PHONY: clean

MACROS_FILES := \
	forCTAN/ed/ed.sty \
	forCTAN/proposal/etc/workaddress.sty \
	forCTAN/proposal/etc/sref.sty \
	forCTAN/proposal/etc/metakeys.sty \
	fromCTAN/etoolbox/etoolbox.sty \
	fromCTAN/hyperref/kvoptions.sty \
	fromCTAN/logreq/logreq.sty \
	fromCTAN/logreq/logreq.def \
	fromCTAN/svninfo.sty \
	fromCTAN/xkeyval.sty \
	forCTAN/proposal/eu/eupdata.sty \

EXTRA_FILES := \
	forCTAN/proposal/eu/euproposal.cls \
	forCTAN/proposal/base/proposal.cls \
	forCTAN/proposal/base/pdata.sty \

macros_download: macros_clean
	tar xvfz macros.tgz

.PHONY: macros_download

macros_clean:
	chmod a+w macros
	rm -rf macros

.PHONY: macros_clean

macros_install: uninstall
	mkdir -p $(TEXMF)
	cd macros && install $(MACROS_FILES) $(TEXMF)
	mkdir -p ${TARGET_DIR}
	$(CP) macros/forCTAN/proposal/* ${TARGET_DIR}

.PHONY: macros_install

PROP_DIR := proposal
PROP_ZIP := $(PROP_DIR).zip
PROP_URL := http://www.tex.ac.uk/CTAN/macros/latex/contrib/$(PROP_ZIP)

prop_diff:
	diff -u -r $(PROP_DIR) $(PROP_DIR).new > $(PROP_DIR).patch || true

.PHONY: prop_diff

prop_download: prop_clean
	unzip $(PROP_ZIP)
	patch -p0 < $(PROP_DIR).patch

.PHONY: prop_download

prop_clean:
	chmod a+w $(PROP_DIR)
	rm -rf $(PROP_DIR)

.PHONY: prop_clean

PROP_FILES := \
	eu/euproposal.cls \
	base/proposal.cls \
	base/pdata.sty \

prop_install:
	mkdir -p $(TEXMF)
	mkdir -p ${TARGET_DIR}
	for i in $(PROP_FILES); do \
		install $(PROP_DIR)/$$i $(TEXMF); \
		DIR=`dirname $$i`; \
		mkdir -p ${TARGET_DIR}/$$DIR; \
		$(CP) $(PROP_DIR)/$$i ${TARGET_DIR}/$$i; \
	done

.PHONY: prop_install

uninstall:
	rm -rf ${TARGET_DIR}

.PHONY: uninstall

