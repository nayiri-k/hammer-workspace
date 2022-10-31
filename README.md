# Hammer Workspace for Simple RTL Designs


## Setup

Create links to your Hammer repo and commercial CAD plugins (if using):

    ln -s <path-to-hammer> hammer
    ln -s <path-to-hammer-cadence-plugins>  hammer-cadence-plugins
    ln -s <path-to-hammer-mentor-plugins>   hammer-mentor-plugins
    ln -s <path-to-hammer-synopsys-plugins> hammer-synopsys-plugins

Run this in every new terminal (or add to your `.bashrc` but use absolute paths instead of `$(pwd)`):

    export HAMMER_HOME=$(pwd)/hammer
    source $HAMMER_HOME/sourceme.sh

Alternatively, just run `source sourceme.sh` in this directory.

## Machine-Specific Setup

This repo is configured to work specifically on the BWRC servers. Here are the changes made:

If using the commercial tool flow, you may need to update the `bwrc-env.yml` file to point to the updated/correct tool licenses on the BWRC servers, or the licenses on whatever machine you are using.

If using the Sky130 technology, in `tech-sky130.yml`:

    technology.sky130:
        sky130B: "/path/to/sky130B"
        openram_lib: "/path/to/sky130_sram_macros"
        # Optional
        sky130_nda: "/path/to/skywater-src-nda"

If using the Asap7 technology, in `tech-asap7.yml`:

    technology.asap7.tarball_dir: "/path/to/asap7"


For the open-source EDA tools, either add to Yosys/OpenROAD to your PATH (ideally in your `.bashrc`), or uncomment the absolute paths to the tool binaries in the respective `tools-*.yml` files:
    synthesis.yosys.yosys_bin: "yosys"
    # on BWRC (only on bwrcr720-3 machine):
    # synthesis.yosys.yosys_bin: "/usr/local/bin/yosys"

    par.openroad.openroad_bin: "openroad"  
    # on BWRC:
    # par.openroad.openroad_bin: "/tools/B/tools/OpenROAD/OpenROAD_20221028/local/bin/openroad"

## VLSI Flow

Run the following commands:

    make syn
    make par
    make drc
    make lvs

And append any of the following Make variables (first one is default):

    tech_name=[sky130,asap7]
    tools_name=[commercial,openroad,yosys]
    
NOTE: haven't verified any of this flow with asap7 configuration yet.

## Simulation
Run the following commands:

    make sim-rtl
    make sim-gl-syn
    make sim-gl-par
