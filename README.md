# Information about your project

The goal of this project is to implement a delay-based physically unclonable function (PUF) in silicon with open source tools.

At the moment, fine control over routing length or propagation delays hasn't been achieved, which will likely produce a PUF with little to no variability among devices. Nonetheless, placing several of them in the same die will almost certainly produce different results *within* the same chip. Therefore, as a proof of concept, four 8-bit DelayPUFs are instantiated to explore how different placement/routing yields distinct function outputs. 

# Build subtleties
In order to prevent optimization of the technology cells I want to force, the argument `-icells` has to be supplied to yosys for synthesis. It enables recognizing modules starting with `$` as internal cells, which is what we need. To "inject" the extra argument, I had to modify the openlane flow `synth.tcl` and allow it to take in the environment variable `READ_VERILOG_OPTS`. The modified script is at `custom/synth.tcl` and shall replace `openlane/scripts/synth.tcl`.

The variable should be set in the project's config.tcl (e.g. `set ::env(READ_VERILOG_OPTS) {icells}`)

# Simulation
`make all` will run the testbech. However, the first two lines of DelayPUF.v have to be uncommented to enable `define SIM` (but commented back for synthesis!) 

I'm sure there's a more elegant way

# License

This project is [licensed under Apache 2](LICENSE)
