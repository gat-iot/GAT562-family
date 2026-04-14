# GAT562 30S Mesh Module

## 产品简介

GAT562 30S Mesh Module 是 GAT562 系列的高功率增强版本，LoRa 发射功率提升至 **30 dBm（1 W）**，相比标准版的 22 dBm，通信距离大幅提升，是超远距离通信和太阳能中继的首选。

> **核心硬件**：nRF52840 + SX1262 + TCXO + 外置 PA，**与 RAK4631 模组 IO 完全兼容，可直接烧录 RAK4631 全系列固件**。

## 快速导航

| 文档 | 说明 |
|------|------|
| [概述](./Overview/) | 产品介绍、核心参数、产品系列 |
| [数据手册](./Datasheet/) | 完整技术规格、电气参数、封装信息 |
| [快速入门](./Quickstart/) | 环境搭建、固件烧录、开发指南 |

## 核心参数对比

| 参数 | GAT562 30S | GAT562 标准版 |
|------|-----------|-------------|
| LoRa 发射功率 | **30 dBm (1 W)** | 22 dBm (158 mW) |
| 通信距离 | 15 km+ | 8-15 km |
| 峰值电流 | ~900 mA | ~200 mA |
| 供电电压 | 3.3-5 V | 2.0-3.6 V |
| 推荐应用 | 远距离/中继站 | 手持/传感节点 |

## 相关链接

- GitHub: [gat-iot/GAT562-family](https://github.com/gat-iot/GAT562-family)
- Meshtastic: [meshtastic.org](https://meshtastic.org)
- 自定义固件: [gat-iot/meshtastic_fw](https://github.com/gat-iot/meshtastic_fw)
