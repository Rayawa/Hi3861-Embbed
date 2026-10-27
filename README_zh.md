# Hi3861-Embbed

[English](README.md) | 简体中文

面向 Hi3861 的 OpenHarmony C 示例，涵盖 GPIO、传感器、显示与自定义 AT 指令。

归档项目，保留用于参考。

## 项目概述

示例覆盖交通灯与按钮、PWM 灯光和蜂鸣器、环境传感器、OLED 输出及 AT 指令计算器。通过 GN 文件选择应用和源文件；本仓库为应用组件，不是完整操作系统源码。

## 技术栈与依赖

C、OpenHarmony Lite、CMSIS-RTOS2、Hi3861 平台接口及 GN/Ninja。需要匹配的 OpenHarmony 源码和工具链、Hi3861 开发板、串口驱动及烧录工具；各示例另需对应传感器或扩展板。

## 文件结构

- `BUILD.gn` — 应用构建入口
- `rayawa/hello/` — 基础任务
- `rayawa/traffic_light/` — 交通灯与按钮
- `rayawa/colorful_light/` — PWM 与感知示例
- `rayawa/environment/` — 环境传感器与 OLED
- `rayawa/at_command/` — 计算器指令
- `samgr/` — 服务管理示例

## 快速上手

1. 将文件集成到兼容的 OpenHarmony Hi3861 应用树中，常见位置为 `applications/sample/wifi-iot/app/`。
2. 编辑 `rayawa/BUILD.gn`，只启用一个示例模块；在模块的 `BUILD.gn` 中选择目标源文件，避免同时启用冲突示例。
3. 在 OpenHarmony 工作区根目录执行 `hb set` 选择对应产品，再执行 `hb build`。
4. 按开发板流程烧录镜像并检查串口输出。现有指南使用 115200 波特率、8 位数据、无校验、1 位停止位。
