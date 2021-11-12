# Build subtleties
In order to prevent optimization of the technology cells I want to force, the argument `-icells` has to be supplied to yosys for synthesis. It enables recognizing modules starting with `$` as internal cells, which is what we need. To "inject" the extra argument, I had to modify the openlane flow `synth.tcl` and allow it to take in the environment variable `READ_VERILOG_OPTS`. The variable can be set in the project's config.tcl (e.g. `set ::env(READ_VERILOG_OPTS) {icells}`)

# Simulation
`make all` will run the testbech. However, the first two lines of DelayPUF.v have to be uncommented to enable `define SIM` (I'm sure there's a more elegant way)

# Information about your project

Four 8-bit DelayPUFs are instantiated to explore how different placement/rounting yields different function outputs. (expand...)

# Project info.yaml

You need to fill in the fields of [info.yaml](info.yaml)

See [here for more information](https://github.com/mattvenn/multi_project_tools/blob/main/docs/project_spec.md)

# License

This project is [licensed under Apache 2](LICENSE)
