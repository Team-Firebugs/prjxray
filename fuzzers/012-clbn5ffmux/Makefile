N := 1
SPECIMENS := $(addprefix specimen_,$(shell seq -f '%03.0f' $(N)))
SPECIMENS_OK := $(addsuffix /OK,$(SPECIMENS))

database: $(SPECIMENS_OK)
	${XRAY_SEGMATCH} -o seg_clblx.segbits $(addsuffix /segdata_clbl[lm]_[lr].txt,$(SPECIMENS))

pushdb:
	${XRAY_MERGEDB} clbll_l seg_clblx.segbits
	${XRAY_MERGEDB} clbll_r seg_clblx.segbits
	${XRAY_MERGEDB} clblm_l seg_clblx.segbits
	${XRAY_MERGEDB} clblm_r seg_clblx.segbits

$(SPECIMENS_OK):
	bash generate.sh $(subst /OK,,$@)
	touch $@

clean:
	rm -rf specimen_[0-9][0-9][0-9]/ seg_clblx.segbits vivado*.log vivado_*.str vivado*.jou design *.bits *.dcp *.bit top.v

.PHONY: database pushdb clean

