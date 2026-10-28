# Hi3861 OpenHarmony Embedded Development Project

English | [简体中文](README_zh.md)


An OpenHarmony embedded-development practice project for the Huawei HiSilicon Hi3861 board, covering four complete modules: traffic lights, multicolor lighting, environmental monitoring and AT commands.

## 📁 Repository Structure

```
Hi3861/
├── rayawa/                         # 核心开发模块
│   ├── hello/                      # 基础示例
│   │   ├── BUILD.gn                # 编译配置
│   │   └── hello.c                 # Hello World 程序
│   │
│   ├── traffic_light/              # 模块一：红绿灯板开发
│   │   ├── BUILD.gn                # 编译配置（一次只能激活一个文件）
│   │   ├── light.c                 # 红黄绿三色灯基础控制
│   │   ├── traffic.c               # 交通灯系统（自动时序）
│   │   ├── ability.c               # 多线程并发开发
│   │   ├── button.c                # S3 按钮开发
│   │   └── control.c               # 按钮控制红绿灯（综合项目）
│   │
│   ├── colorful_light/             # 模块二：炫彩灯板开发
│   │   ├── BUILD.gn                # 编译配置
│   │   ├── beep.c                  # 蜂鸣器控制
│   │   ├── music.c                 # 蜂鸣器音乐播放
│   │   ├── led.c                   # 混合音乐与三色灯（音乐可视化）
│   │   ├── human_sensor.c          # 人体红外热释电传感器
│   │   ├── photosensitive.c        # 光敏电阻开发
│   │   └── human_sensor_light.c    # 夜晚人体感应灯（综合项目）
│   │
│   ├── environment/                # 模块三：环境监测板开发
│   │   ├── BUILD.gn                # 编译配置
│   │   ├── mq2_demo.c              # MQ-2 燃气传感器开发
│   │   ├── aht20.c/.h              # AHT20 温湿度传感器驱动
│   │   ├── aht20_demo.c            # AHT20 传感器演示
│   │   ├── oled_ssd1306.c/.h       # OLED 显示屏驱动
│   │   ├── oled_fonts.h            # OLED 字体库
│   │   ├── oled_demo.c             # OLED 显示演示
│   │   └── enrionment_demo.c       # 综合环境监测系统
│   │
│   └── at_command/                 # 模块四：AT 指令开发
│       ├── BUILD.gn                # 编译配置
│       └── cal.c                   # 自定义 AT+CALC 指令
│
├── demolink/                        # 基础链接示例
├── iothardware/                     # IoT 硬件示例
├── samgr/                           # 系统服务管理
└── startup/                         # 启动配置
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
light.c（基础） → traffic.c（系统） → ability.c（并发） → button.c（交互） → control.c（综合）
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
beep.c（声音） → music.c（音乐） → led.c（可视化） → human_sensor.c（感知） → photosensitive.c（环境） → human_sensor_light.c（智能）
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
# traffic_light/BUILD.gn 示例
sources = [
    "light.c",    # 激活基础灯控制
    # "traffic.c",  # 注释其他文件
    # "ability.c",
    # "button.c",
    # "control.c",
]
```

### **Top-Level Build Configuration**
```gn
# rayawa/BUILD.gn - 控制激活的模块
features = [
    "hello:hello",                    # 基础示例
    "traffic_light:traffic_light",    # 红绿灯模块
    # "colorful_light:colorful_light", # 注释不需要的模块
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
# 确保 OpenHarmony 开发环境已配置
# Hi3861 开发板连接正常
# 串口驱动安装完成
```

### **2. Build the First Program**
```bash
# 激活 hello 模块
cd rayawa
# 编辑 BUILD.gn，只保留 "hello:hello"

# 编译
cd ../../  # 回到 OpenHarmony 根目录
hb build

# 烧录测试
# 使用 HiBurn 烧录，串口查看 "Hello OpenHarmony!"
```

### **3. Further Development**
```bash
# 切换到红绿灯模块
# 1. 编辑 rayawa/BUILD.gn，激活 traffic_light
# 2. 编辑 traffic_light/BUILD.gn，激活 light.c
# 3. 重新编译烧录
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
