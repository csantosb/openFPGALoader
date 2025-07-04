# openFPGALoader

<p align="right">
  <a title="Documentation" href="https://trabucayre.github.io/openFPGALoader"><img src="https://img.shields.io/website.svg?label=trabucayre.github.io%2FopenFPGALoader&longCache=true&style=flat-square&url=http%3A%2F%2Ftrabucayre.github.io%2FopenFPGALoader%2Findex.html&logo=GitHub"></a><!--
  -->
  <a title="'Test' workflow Status" href="https://github.com/trabucayre/openFPGALoader/actions/workflows/Test.yml"><img alt="'Test' workflow Status" src="https://img.shields.io/github/actions/workflow/status/trabucayre/openFPGALoader/Test.yml?branch=master&longCache=true&style=flat-square&label=Test&logo=github%20actions&logoColor=fff"></a><!--
  -->
  <a title="Releases" href="https://github.com/trabucayre/openFPGALoader/releases"><img src="https://img.shields.io/github/commits-since/trabucayre/openFPGALoader/latest.svg?longCache=true&style=flat-square&logo=git&logoColor=fff"></a>
</p>

<p align="center">
  <strong><a href="https://trabucayre.github.io/openFPGALoader/guide/first-steps.html">First steps</a> • <a href="https://trabucayre.github.io/openFPGALoader/guide/install.html">Install</a> • <a href="https://trabucayre.github.io/openFPGALoader/guide/troubleshooting.html">Troubleshooting</a></strong> • <a href="https://trabucayre.github.io/openFPGALoader/guide/advanced.html">Advanced usage</a>
</p>

Universal utility for programming FPGAs. Compatible with many boards, cables and FPGA from major manufacturers (Xilinx, Altera/Intel, Lattice, Gowin, Efinix, Anlogic, Cologne Chip). openFPGALoader works on Linux, Windows and macOS.

Not sure if your hardware is supported? Check the hardware compatibility lists:

 * [FPGA compatibility list](https://trabucayre.github.io/openFPGALoader/compatibility/fpga.html)
 * [Board compatibility list](https://trabucayre.github.io/openFPGALoader/compatibility/board.html)
 * [Cable compatibility list](https://trabucayre.github.io/openFPGALoader/compatibility/cable.html)

Also checkout the vendor-specific documentation:
[Anlogic](https://trabucayre.github.io/openFPGALoader/vendors/anlogic.html),
[Cologne Chip](https://trabucayre.github.io/openFPGALoader/vendors/colognechip.html),
[Efinix](https://trabucayre.github.io/openFPGALoader/vendors/efinix.html),
[Gowin](https://trabucayre.github.io/openFPGALoader/vendors/gowin.html),
[Intel/Altera](https://trabucayre.github.io/openFPGALoader/vendors/intel.html),
[Lattice](https://trabucayre.github.io/openFPGALoader/vendors/lattice.html),
[Xilinx](https://trabucayre.github.io/openFPGALoader/vendors/xilinx.html).

OpenFPGALoader has a dedicated channel: [#openFPGALoader at libera.chat](https://web.libera.chat/#openFPGALoader).

## Quick Usage

`arty` in the example below is one of the many FPGA board configurations listed [here](https://trabucayre.github.io/openFPGALoader/compatibility/board.html).

```bash
openFPGALoader -b arty arty_bitstream.bit # Loading in SRAM
openFPGALoader -b arty -f arty_bitstream.bit # Writing in flash
```

You can also specify a JTAG cable model (complete list [here](https://trabucayre.github.io/openFPGALoader/compatibility/cable.html)) instead of the board model:

```bash
openFPGALoader -c cmsisdap fpga_bitstream.bit
```

## Usage

```
Usage: ./openFPGALoader [OPTION...] BIT_FILE
openFPGALoader -- a program to flash FPGA

      --altsetting arg          DFU interface altsetting (only for DFU mode)
      --bitstream arg           bitstream
      --secondary-bitstream arg
                                secondary bitstream (some Xilinx UltraScale
                                boards)
  -b, --board arg               board name, may be used instead of cable
  -B, --bridge arg              disable spiOverJtag model detection by
                                providing bitstream(intel/xilinx)
  -c, --cable arg               jtag interface
      --status-pin arg          JTAG mode / FTDI: GPIO pin number to use as a
                                status indicator (active low)
      --invert-read-edge        JTAG mode / FTDI: read on negative edge
                                instead of positive
      --vid arg                 probe Vendor ID
      --pid arg                 probe Product ID
      --cable-index arg         probe index (FTDI and cmsisDAP)
      --busdev-num arg          select a probe by it bus and device number
                                (bus_num:device_addr)
      --ftdi-serial arg         FTDI chip serial number
      --ftdi-channel arg        FTDI chip channel number (channels 0-3 map to
                                A-D)
  -d, --device arg              device to use (/dev/ttyUSBx)
      --detect                  detect FPGA, add -f to show connected flash
      --dfu                     DFU mode
      --dump-flash              Dump flash mode
      --bulk-erase              Bulk erase flash
      --enable-quad             Enable quad mode for SPI Flash
      --disable-quad            Disable quad mode for SPI Flash
      --target-flash arg        for boards with multiple flash chips (some
                                Xilinx UltraScale boards), select the target
                                flash: primary (default), secondary or both
      --external-flash          select ext flash for device with internal and
                                external storage
      --file-size arg           provides size in Byte to dump, must be used
                                with dump-flash
      --file-type arg           provides file type instead of let's deduced
                                by using extension
      --flash-sector arg        flash sector (Lattice and Altera MAX10 parts
                                only)
      --fpga-part arg           fpga model flavor + package
      --freq arg                jtag frequency (Hz)
  -f, --write-flash             write bitstream in flash (default: false)
      --index-chain arg         device index in JTAG-chain
      --misc-device arg         add JTAG non-FPGA devices <idcode,irlen,name>
      --ip arg                  IP address (XVC and remote bitbang client)
      --list-boards             list all supported boards
      --list-cables             list all supported cables
      --list-fpga               list all supported FPGA
  -m, --write-sram              write bitstream in SRAM (default: true)
  -o, --offset arg              Start address (in bytes) for read/write into
                                non volatile memory (default: 0)
      --pins arg                pin config TDI:TDO:TCK:TMS or
                                MOSI:MISO:SCK:CS[:HOLDN:WPN]
      --probe-firmware arg      firmware for JTAG probe (usbBlasterII)
      --protect-flash arg       protect SPI flash area
      --quiet                   Produce quiet output (no progress bar)
  -r, --reset                   reset FPGA after operations
      --scan-usb                scan USB to display connected probes
      --skip-load-bridge        skip writing bridge to SRAM when in
                                write-flash mode
      --skip-reset              skip resetting the device when in write-flash
                                mode
      --spi                     SPI mode (only for FTDI in serial mode)
      --unprotect-flash         Unprotect flash blocks
  -v, --verbose                 Produce verbose output
      --verbose-level arg       verbose level -1: quiet, 0: normal,
                                1:verbose, 2:debug
  -h, --help                    Give this help list
      --verify                  Verify write operation (SPI Flash only)
      --xvc                     Xilinx Virtual Cable Functions
      --port arg                Xilinx Virtual Cable and remote bitbang Port
                                (default 3721)
      --mcufw arg               Microcontroller firmware
      --conmcu                  Connect JTAG to MCU
  -D, --read-dna                Read DNA (Xilinx FPGA only)
  -X, --read-xadc               Read XADC (Xilinx FPGA only)
      --read-register arg       Read Status Register(Xilinx FPGA only)
      --user-flash arg          User flash file (Gowin LittleBee FPGA only)
  -V, --Version                 Print program version

Mandatory or optional arguments to long options are also mandatory or optional
for any corresponding short options.

Report bugs to <gwenhael.goavec-merou@trabucayre.com>.
```

By default **spiOverJtag** are search into `${CMAKE_INSTALL_FULL_DATAROOTDIR}`
(*/usr/local/share/* by default). It's possible to change this behaviour by
using an environment variable:

```bash
export OPENFPGALOADER_SOJ_DIR=/somewhere
openFPGALoader xxxx
```

or

```
OPENFPGALOADER_SOJ_DIR=/somewhere openFPGALoader xxxx
```

`OPENFPGALOADER_SOJ_DIR` must point to directory containing **spiOverJtag**
bitstreams.

## Sponsors/Partners

![Sponsors](https://github.com/user-attachments/assets/cb4efce1-ed0c-461c-bd05-9caeb440870d)
