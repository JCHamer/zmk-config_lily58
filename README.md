# ZMK Configuration for building a Lily58 with RGB LEDs

This configuration is aimed at a MiFunny/[PandaKB Lily58 Kit](https://pandakb.com/build-guides/lily58-rgb-mx-build-guide/) with a nrf52840 ProMicro

## Building Keyboard Files
Configurations can be built using GitHub actions that are run upon pushing a commit and can then be fetched from Github actions results.

Alternatively, the primary ZMK and Zephyr tools can be fetched and used to locally build a keyboard configuration. This process can be done by following the [zmk native setup](https://zmk.dev/docs/development/local-toolchain/setup/native) documentation. Which inculded installing `cmake`, `python`, `dtc`, and `zephyr-sdk` using the system package manager. You'll also need to install a few python packages to properly build zmk_studio support with the command `pip install protobuf grpcio-tools` from inside the python virtual environment. After cloning the zmk repo and running through the whole setup process, a specific keyboard configuration can then be built by developing the correct [cmake/west command](https://zmk.dev/docs/development/local-toolchain/build-flash?build-opts=addonMcu). For example, to build this keyboard you may use a pair of commands like the following:

```
$ cd /path/to/zmk/source/repo/zmk
$ source .venv/bin/activate
$ cd app
$ west build -d build/left -b nice_nano_v2 -S studio-rpc-usb-uart -- -DSHIELD=lily58_left -DZMK_CONFIG="/path/to/this/repo/zmk-config_lily58/config" -DCONFIG_ZMK_STUDIO=y
$ west build -d build/right -b nice_nano_v2 -- -DSHIELD=lily58_right -DZMK_CONFIG="/path/to/this/repo/zmk-config_lily58/config"
```

As an additional note, the path to this repo in the west build command must be a complete path, `~/` cannot be used. If needed, these commands can also be run with the `-p` flag in order to run a "pristine" build that will clean out the build dir first.

## Flashing Keyboard halves
After having built your configuration, either via Github actions or locally, you'll end up with a left and a right `.uf2` file, you'll plug in a keyboard half, doucle-click the reset button to enter the bootloader mode (or press a software-mapped bootloader button) and copy the corresponding `uf2` file to the `NICE_NANO` USB drive that shows up.

## Configuring a New Keyboard
Follow the instructions from [ZMK](https://zmk.dev/docs/user-setup), this repo was configured by selecting 44:Lily58, 10:nice_nano_v2, and copying in the stock keymap to begin customizations.


