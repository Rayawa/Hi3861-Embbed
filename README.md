# Hi3861-Embbed

English | [简体中文](README_zh.md)

OpenHarmony C examples for Hi3861 GPIO, sensors, displays and custom AT commands.

Archived project retained for reference.

## Overview

The examples cover traffic lights and buttons, PWM lighting and buzzers, environmental sensors, OLED output and an AT-command calculator. GN files select the active application and source files; this repository is an application component rather than a complete operating-system checkout.

## Technology and Dependencies

C, OpenHarmony Lite, CMSIS-RTOS2, Hi3861 platform APIs and GN/Ninja. A matching OpenHarmony source/toolchain, a Hi3861 board, serial drivers and a compatible flashing utility are required. Individual examples need their corresponding sensor or extension board.

## Repository Structure

- `BUILD.gn` — top-level application target
- `rayawa/hello/` — basic task example
- `rayawa/traffic_light/` — lights and buttons
- `rayawa/colorful_light/` — PWM and sensing examples
- `rayawa/environment/` — environmental sensors and OLED
- `rayawa/at_command/` — custom calculator command
- `samgr/` — service-manager examples

## Quick Start

1. Integrate these files into the compatible OpenHarmony Hi3861 application tree, commonly `applications/sample/wifi-iot/app/`.
2. Edit `rayawa/BUILD.gn` to enable one example module. In its `BUILD.gn`, select the intended source rather than enabling conflicting demos together.
3. From the OpenHarmony workspace root, select the matching product with `hb set`, then run `hb build`.
4. Flash the generated image using the board's flashing workflow and inspect its serial output. The existing guide uses 115200 baud, 8 data bits, no parity and 1 stop bit.
