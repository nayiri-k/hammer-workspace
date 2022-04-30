# Hammer Workspace for Simple RTL Designs

### VLSI Flow

First create links to your Hammer repo and commercial CAD plugins (if using):
    ln -s <path-to-hammer> hammer
    ln -s <path-to-hammer-cadence-plugins> hammer-cadence-plugins
    ln -s <path-to-hammer-mentor-plugins> hammer-mentor-plugins/
    ln -s <path-to-hammer-synopsys-plugins> hammer-synopsys-plugins/

Run the following commands:
    make syn
    make par
    make drc
    make lvs

And append any of the following Make variables (first one is default):
    tech_name=[sky130,asap7]
    tools_name=[commercial,openroad,yosys]
NOTE: haven't verified any of this flow with asap7 configuration yet.

### Simulation
Run the following commands:
    make sim-rtl
    make sim-gl-syn
    make sim-gl-par