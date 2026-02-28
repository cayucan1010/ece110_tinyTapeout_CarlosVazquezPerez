![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg) ![](../../workflows/test/badge.svg) ![](../../workflows/fpga/badge.svg)

# Tiny Tapeout Verilog Project Template

- [Read the documentation for project](docs/info.md)

## What is Tiny Tapeout?

Tiny Tapeout is an educational project that aims to make it easier and cheaper than ever to get your digital and analog designs manufactured on a real chip.

To learn more and get started, visit https://tinytapeout.com.

## Set up your Verilog project

1. Add your Verilog files to the `src` folder.
2. Edit the [info.yaml](info.yaml) and update information about your project, paying special attention to the `source_files` and `top_module` properties. If you are upgrading an existing Tiny Tapeout project, check out our [online info.yaml migration tool](https://tinytapeout.github.io/tt-yaml-upgrade-tool/).
3. Edit [docs/info.md](docs/info.md) and add a description of your project.
4. Adapt the testbench to your design. See [test/README.md](test/README.md) for more information.

The GitHub action will automatically build the ASIC files using [LibreLane](https://www.zerotoasiccourse.com/terminology/librelane/).

## Enable GitHub actions to build the results page

- [Enabling GitHub Pages](https://tinytapeout.com/faq/#my-github-action-is-failing-on-the-pages-part)

## Resources

- [FAQ](https://tinytapeout.com/faq/)
- [Digital design lessons](https://tinytapeout.com/digital_design/)
- [Learn how semiconductors work](https://tinytapeout.com/siliwiz/)
- [Join the community](https://tinytapeout.com/discord)
- [Build your design locally](https://www.tinytapeout.com/guides/local-hardening/)

## My readme
This project, created by Carlos Vazquez Perez following Professor Eshraghian's lectures, implements a simple Leaky Integrate-and-Fire (LIF) neuron in Verilog on a single Tiny Tapeout tile. Each clock cycle, the neuron accumulates an 8-bit input current supplied through pins `ui[0:7]` while its internal membrane state decays by half via a right bit-shift, mimicking biological charge leakage. When the membrane state reaches or exceeds a threshold of 200, the neuron fires a spike. The full membrane state is readable at any time through output pins `uo[0:7]`, and the spike signal is exposed on `uio[7]`.

The cocotb Python testbench verifies the design by resetting the neuron, feeding it a sustained current of 200 on the input pins, and confirming after enough clock cycles that the spike output is high (`uio_out == 128`, meaning bit 7 is set). The design is split across two source files, `tt_um_lif.v` and `lif.v`, where the former is the Tiny Tapeout wrapper and the latter contains the core neuron logic.
