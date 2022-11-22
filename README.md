![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg)

# Tiny Tapeout 2: Gold code generator and Fibonacci sequence

This project has been migrated from
[https://github.com/daniestevez/tinytapeout-verilog], which was submitted to
Tiny Tapeout 1.

## Description

This project includes two independent designs: a design that calculates terms of
the Fibonacci sequence and displays them in hex one character at a time on a
7-segment display, and a Gold code generator that generates the codes used by
CCSDS X-band PN Delta-DOR.

## How it works

The Fibonacci calculator uses 56-bit integers, so the terms of the Fibonacci
sequence are displayed using 7 hex characters. Since the TinyTapeout PCB only
has one 7-segment display, the terms of the Fibonacci sequence are displayed one
hex character at a time, in LSB order. The dot of the 7-segment display lights
up whenever the LSB is being displayed. On each clock cycle, 4-bits of the next
Fibonacci term are calculated using a 4-bit adder, and 4-bits of the current
term are displayed in the 7-segment display. The 7-segment display is ANDed with
the project clock, so that the digits flash on the display.

The Gold code generator computes a CCSDS X-band PN Delta-DOR Gold code one bit
at a time using LFSRs. The output bit is shown on the 7-segment display
dot. 6-bits of the second LFSR can be loaded in parallel using 6 project inputs
in order to be able to generate different sequences. One of the project inputs
is used to select whether the 7-segment display dot is driven by the Fibonacci
calculator or by the Gold code generator.

## How to test

The project can be tested by manually driving the clock using a push button or
switch. Just by de-asserting the reset and driving the clock, the digits of the
Fibonacci sequence terms should appear on the 7-segment display. The output
select input needs to be set to Gold code (high level) in order to test the gold
code generator. The load enable input (active-low), as well as the 6 inputs
corresponding to the load for the B register can be used to select the sequence
to generate. The load value can be set in the 6 load inputs, and then the load
enable should be pulsed to perform the load. This can be done with the clock
running or stopped, as the load enable is asynchronous. After the load enable is
de-asserted, for each clock cycle a new bit of the Gold code sequence should
appear in the 7-segment display dot.

# What is Tiny Tapeout?

TinyTapeout is an educational project that aims to make it easier and cheaper than ever to get your digital designs manufactured on a real chip!

Go to https://tinytapeout.com for instructions!

## How to change the Wokwi project

Edit the [info.yaml](info.yaml) and change the wokwi_id to match your project.

## How to enable the GitHub actions to build the ASIC files

Please see the instructions for:

* [Enabling GitHub Actions](https://tinytapeout.com/faq/#when-i-commit-my-change-the-gds-action-isnt-running)
* [Enabling GitHub Pages](https://tinytapeout.com/faq/#my-github-action-is-failing-on-the-pages-part)

## How does it work?

When you edit the info.yaml to choose a different ID, the [GitHub Action](.github/workflows/gds.yaml) will fetch the digital netlist of your design from Wokwi.

After that, the action uses the open source ASIC tool called [OpenLane](https://www.zerotoasiccourse.com/terminology/openlane/) to build the files needed to fabricate an ASIC.

## Resources

* [FAQ](https://tinytapeout.com/faq/)
* [Digital design lessons](https://tinytapeout.com/digital_design/)
* [Join the community](https://discord.gg/rPK2nSjxy8)

## What next?

* Share your GDS on Twitter, tag it [#tinytapeout](https://twitter.com/hashtag/tinytapeout?src=hashtag_click) and [link me](https://twitter.com/matthewvenn)!
