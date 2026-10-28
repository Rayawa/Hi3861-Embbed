# Hi3861 OpenHarmony Embedded Development Project

English | [简体中文](README_zh.md)


An OpenHarmony embedded-development practice project for the Huawei HiSilicon Hi3861 board, covering four complete modules: traffic lights, multicolor lighting, environmental monitoring and AT commands.

## 📁 Repository Structure

```
Hi3861/
├── rayawa/                         # Core development modules
│   ├── hello/                      # Basic example
│   │   ├── BUILD.gn                # Build configuration
│   │   └── hello.c                 # Hello World program
│   │
│   ├── traffic_light/              # Module 1: Traffic light board
│   │   ├── BUILD.gn                # Build configuration (only one file active at a time)
│   │   ├── light.c                 # Basic red/yellow/green light control
│   │   ├── traffic.c               # Traffic light system (automatic timing)
│   │   ├── ability.c               # Multithreaded concurrency
│   │   ├── button.c                # S3 button
│   │   └── control.c               # Button-controlled traffic lights (integrated project)
│   │
│   ├── colorful_light/             # Module 2: Colorful light board
│   │   ├── BUILD.gn                # Build configuration
│   │   ├── beep.c                  # Buzzer control
│   │   ├── music.c                 # Buzzer music playback
│   │   ├── led.c                   # Music and three-color lights (music visualization)
│   │   ├── human_sensor.c          # PIR human sensor
│   │   ├── photosensitive.c        # Photoresistor
│   │   └── human_sensor_light.c    # Nighttime motion-sensing light (integrated project)
│   │
│   ├── environment/                # Module 3: Environment monitoring board
│   │   ├── BUILD.gn                # Build configuration
│   │   ├── mq2_demo.c              # MQ-2 gas sensor
│   │   ├── aht20.c/.h              # AHT20 temperature/humidity driver
│   │   ├── aht20_demo.c            # AHT20 sensor demo
│   │   ├── oled_ssd1306.c/.h       # OLED display driver
│   │   ├── oled_fonts.h            # OLED fonts
│   │   ├── oled_demo.c             # OLED display demo
│   │   └── enrionment_demo.c       # Integrated environment monitoring
│   │
│   └── at_command/                 # Module 4: AT commands
│       ├── BUILD.gn                # Build configuration
│       └── cal.c                   # Custom AT+CALC command
│
├── demolink/                        # Basic linking example
├── iothardware/                     # IoT hardware examples
├── samgr/                           # System service management
└── startup/                         # Startup configuration
```

## 🎯 Detailed Guide to the Four Modules

### **Module 1: Traffic-Light Board** 🚦

#### **Hardware Configuration**
- **Three-color LEDs**: GPIO_10 (red), GPIO_11 (green), GPIO_12 (yellow)
- **Control button**: GPIO_8 (S3 button)

#### **Examples**
1. **`light.c`** - Basic light control
   - Switching individual LEDs on and off
   - Combined control of three-color LEDs
   - Delays and blinking

2. **`traffic.c`** - Traffic-light system
   - Standard sequence: red → green → yellow → red
   - Automatic cycling
   - CMSIS-RTOS2 task scheduling

3. **`ability.c`** - Multithreaded concurrency
   - OpenHarmony multitasking
   - Concurrent task demonstration
   - Inter-task synchronization

4. **`button.c`** - S3 button example
   - GPIO input detection
   - Button debouncing
   - Interrupt and polling modes

5. **`control.c`** - Button-controlled traffic lights (**integrated project**)
   - Switching traffic-light states with a button
   - Manual/automatic mode selection
   - State-machine design

#### **Learning Sequence**
```
light.c (basics) → traffic.c (system) → ability.c (concurrency) → button.c (interaction) → control.c (integration)
```

### **Module 2: Multicolor-Light Board** 🎨

#### **Hardware Configuration**
- **Three-color LEDs**: PWM1 (red), PWM2 (green), PWM3 (yellow)
- **Buzzer**: PWM0
- **Human-presence sensor**: ADC channel 3
- **Photoresistor**: ADC input

#### **Examples**
1. **`beep.c`** - Buzzer control
   - PWM frequency control
   - Generating different tones
   - Alarm sounds

2. **`music.c`** - Buzzer music playback
   - Playing predefined melodies
   - Rhythm and pitch control
   - Multiple songs

3. **`led.c`** - Music with three-color LEDs (**music visualization**)
   - **Main example**: music-rhythm visualization
   - LEDs respond to the music rhythm
   - Multiple lighting effects
   - PWM dimming

4. **`human_sensor.c`** - Infrared human-presence sensor
   - Motion detection
   - ADC acquisition
   - Sensitivity adjustment

5. **`photosensitive.c`** - Photoresistor example
   - Ambient-light measurement
   - Automatic brightness adjustment
   - Day/night detection

6. **`human_sensor_light.c`** - Nighttime motion-activated light (**integrated project**)
   - Automatically turn on the light when motion is detected at night
   - Combine light and presence sensors
   - Delayed shutdown to save energy

#### **Learning Sequence**
```
beep.c (sound) → music.c (music) → led.c (visualization) → human_sensor.c (sensing) → photosensitive.c (environment) → human_sensor_light.c (smart control)
```

### **Module 3: Environmental-Monitoring Board** 🌡️

#### **Hardware Configuration**
- **MQ-2 gas sensor**: ADC channel 5
- **AHT20 temperature/humidity sensor**: I2C
- **OLED display**: SSD1306 over I2C
- **Buzzer alarm**: PWM0

#### **Examples**
1. **`mq2_demo.c`** - Gas sensor
   - Combustible-gas concentration measurement
   - ADC acquisition and conversion
   - Concentration-threshold alarm

2. **`aht20.c/.h`** - Temperature/humidity sensor driver
   - I2C protocol implementation
   - Measurement accuracy: temperature ±0.3°C, humidity ±2%
   - Data-calibration algorithm

3. **`oled_ssd1306.c/.h`** - OLED display driver
   - 128×64 pixel display control
   - Font rendering and graphics
   - Framebuffer management

4. **`oled_demo.c`** - OLED display demonstration
   - Live temperature/humidity display
   - Data-chart rendering
   - Multiple display pages

5. **`enrionment_demo.c`** - Integrated environmental monitoring (**main example**)
   - **Sensor fusion**: temperature, humidity and gas concentration
   - **Live display**: all environmental values on OLED
   - **Automatic alarm**: buzzer when a value exceeds its threshold
   - **Data refresh**: periodic display updates

#### **Technical Features**
- **I2C**: AHT20 and OLED share the I2C bus
- **ADC acquisition**: digitization of the MQ-2 analog signal
- **Live display**: optimized OLED refresh rate
- **Threshold management**: configurable alarm thresholds

### **Module 4: AT Commands** 📡

#### **Example**
1. **`cal.c`** - Custom AT+CALC command
   - **Command format**: `AT+CALC=a,b`
   - **Function**: four-operation calculator
   - **Output**: sum, difference, product and quotient

#### **Features**
- **Parameter validation**: accepts two integer parameters
- **Complete calculation**: returns all four results
- **Error handling**: division-by-zero protection
- **AT framework integration**: integrated into the OpenHarmony AT system

#### **Usage Example**
Example input:
```
AT+CALC=12,3
```
Example output:
```
+CALC:Sum=15
+CALC:Diff=9
+CALC:Prod=36
+CALC:Quot=4
OK
```

## 🛠️ Build and Usage Guide

### **Build Configuration**
Each module's `BUILD.gn` selects the active source files:

```gn
# traffic_light/BUILD.gn example
sources = [
    "light.c",    # Enable basic light control
    # "traffic.c",  # Comment out other files
    # "ability.c",
    # "button.c",
    # "control.c",
]
```

### **Top-Level Build Configuration**
```gn
# rayawa/BUILD.gn - Select active modules
features = [
    "hello:hello",                    # Basic example
    "traffic_light:traffic_light",    # Traffic light module
    # "colorful_light:colorful_light", # Comment out unused modules
    # "environment:environment",
    # "at_command:at_command",
]
```

### **Development Workflow**
1. **Select a module**: enable it in `rayawa/BUILD.gn`.
2. **Select a source file**: enable it in the module's `BUILD.gn`.
3. **Build**: run `hb build` from the OpenHarmony root.
4. **Flash**: use HiBurn to flash the firmware.
5. **Test**: inspect output in a serial terminal at 115200 baud.

### **Serial Debugging**
- **Baud rate**: 115200
- **Data bits**: 8
- **Stop bits**: 1
- **Parity**: none
- **Flow control**: none


## 🔧 Technology

### **Hardware Interfaces**
- **GPIO**: LEDs and buttons
- **PWM**: buzzer and LED dimming
- **I2C**: AHT20 and OLED communication
- **ADC**: MQ-2, presence sensor and photoresistor

### **Software Frameworks**
- **OpenHarmony**: operating system
- **CMSIS-RTOS2**: real-time task scheduling
- **HiAT Framework**: AT-command handling
- **Driver Framework**: hardware-driver abstraction

### **Development Tools**
- **Build system**: GN + Ninja
- **Flashing tool**: HiBurn
- **Debugging tool**: IPOP
- **Version control**: Git

## 🚀 Quick Start

### **1. Prepare the Environment**
```bash
# Ensure the OpenHarmony development environment is configured
# Check the Hi3861 board connection
# Install the serial driver
```

### **2. Build the First Program**
```bash
# Enable the hello module
cd rayawa
# Edit BUILD.gn to retain only "hello:hello"

# Build
cd ../../  # Return to the OpenHarmony root
hb build

# Flash and test
# Flash with HiBurn and check the serial port for "Hello OpenHarmony!"
```

### **3. Further Development**
```bash
# Switch to the traffic light module
# 1. Edit rayawa/BUILD.gn to enable traffic_light
# 2. Edit traffic_light/BUILD.gn to enable light.c
# 3. Rebuild and flash
```

## 🤝 Development Conventions

### **Coding Conventions**
1. **Naming**: use camelCase, with uppercase names for hardware-related constants.
2. **Comments**: document the purpose of important functions.
3. **Error handling**: check errors for all hardware operations.
4. **Resource management**: release dynamically allocated resources.

### **Module Design**
1. **Single responsibility**: each file implements one clear function.
2. **Clear interfaces**: modules communicate through defined interfaces.
3. **Configurability**: select features through BUILD.gn.
4. **Testability**: support testing each feature independently.
