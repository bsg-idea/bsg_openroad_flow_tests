
################################################################################
# TODO: Set the following variables in order to use VCS
#

export LM_LICENSE_FILE :=
export VCS             :=
export VCS_HOME        := $(realpath $(dir $(VCS))../)

#
################################################################################

.DEFAULT_GOAL=run

export THIS_DIR := $(realpath $(shell dirname $(realpath $(lastword $(MAKEFILE_LIST)))))
export TOP_DIR ?= $(shell git rev-parse --show-toplevel)

export BLACKPARROT_DIR   ?= $(THIS_DIR)/black-parrot
export BSG_IP_CORES_DIR  ?= $(THIS_DIR)/bsg_ip_cores
export OPENROAD_FLOW_DIR ?= $(THIS_DIR)/OpenROAD-flow

export BP_COMMON_DIR ?= $(BLACKPARROT_DIR)/bp_common
export BP_TOP_DIR    ?= $(BLACKPARROT_DIR)/bp_top
export BP_FE_DIR     ?= $(BLACKPARROT_DIR)/bp_fe
export BP_BE_DIR     ?= $(BLACKPARROT_DIR)/bp_be
export BP_ME_DIR     ?= $(BLACKPARROT_DIR)/bp_me

export BSG_OUT_DIR := out

export VCS_OPTIONS := +vcs+finish+5000000ps
export VCS_OPTIONS += -timescale=1ps/1ps
export VCS_OPTIONS += -full64
export VCS_OPTIONS += +vcs+lic+wait
export VCS_OPTIONS += +v2k
export VCS_OPTIONS += -sverilog
export VCS_OPTIONS += -debug_pp
export VCS_OPTIONS += +libext+.v+.vlib+.vh
export VCS_OPTIONS += +vcs+vcdpluson
export VCS_OPTIONS += -o simv
export VCS_OPTIONS += -top test_bp
export VCS_OPTIONS += -f $(THIS_DIR)/flist.vcs
export VCS_OPTIONS += $(BP_TOP_DIR)/test/tb/bp_single_trace_demo/test_bp.v
export VCS_OPTIONS += +vcs+initreg+random

export VCS_OPTIONS += -pvalue+vaddr_width_p=56
export VCS_OPTIONS += -pvalue+paddr_width_p=22
export VCS_OPTIONS += -pvalue+asid_width_p=10
export VCS_OPTIONS += -pvalue+branch_metadata_fwd_width_p=36
export VCS_OPTIONS += -pvalue+btb_indx_width_p=9
export VCS_OPTIONS += -pvalue+bht_indx_width_p=5
export VCS_OPTIONS += -pvalue+ras_addr_width_p=22
export VCS_OPTIONS += -pvalue+core_els_p=1
export VCS_OPTIONS += -pvalue+num_cce_p=1
export VCS_OPTIONS += -pvalue+num_lce_p=2
export VCS_OPTIONS += -pvalue+lce_sets_p=64
export VCS_OPTIONS += -pvalue+cce_block_size_in_bytes_p=64
export VCS_OPTIONS += -pvalue+cce_num_inst_ram_els_p=256
export VCS_OPTIONS += -pvalue+lce_assoc_p=8
export VCS_OPTIONS += -pvalue+boot_rom_els_p=512
export VCS_OPTIONS += -pvalue+boot_rom_width_p=512
export VCS_OPTIONS += -pvalue+mem_els_p=512
export VCS_OPTIONS += -pvalue+trace_ring_width_p=129
export VCS_OPTIONS += -pvalue+trace_rom_addr_width_p=32

export VCS_OPTIONS += +warn=all,noOPD,noTMR,noTFIPC
export VCS_OPTIONS += +notimingcheck
export VCS_OPTIONS += +nospecify

export PROG ?=towers

run: | OpenROAD-flow black-parrot bsg_ip_cores
	mkdir -p $(BSG_OUT_DIR)
	cp config.txt $(BSG_OUT_DIR)
	cd $(BSG_OUT_DIR) && $(VCS) $(VCS_OPTIONS) | tee -i build.log
	cd $(BSG_OUT_DIR) && ./simv +vcs+initreg+config+config.txt | tee -i run.log

clean:
	rm -rf $(BSG_OUT_DIR)

OpenROAD-flow:
	git clone git@github.com:stdavids/OpenROAD-flow.git $@_temp
	cd $@_temp ; git checkout b34efb3a1419c07ed1f66c9b98cd9b6d9a4cede7
	mv $@_temp $@

black-parrot:
	git clone git@github.com:black-parrot/black-parrot.git $@_temp
	cd $@_temp ; git checkout 49cce8f1bb9278d4420d559a3e95244029994886
	mv $@_temp $@

bsg_ip_cores:
	git clone git@bitbucket.org:taylor-bsg/bsg_ip_cores $@_temp
	cd $@_temp ; git checkout 5833ee81dcc3e35ee7e9bf06517ed2899e83ac82
	mv $@_temp $@

