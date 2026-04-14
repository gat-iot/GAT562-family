# GAT562 Mesh Module 概述

## 产品简介

GAT562 Mesh Module 是基于 Nordic nRF52840 + Semtech SX1262 一体化设计的 LoRa + BLE 融合模组，**与 RAK4631 模组 IO 完全兼容，可直接烧录 RAK4631 固件**。模组搭配 TCXO 温补有源晶振，性能稳定，接口丰富，预装 Meshtastic 开源固件，开箱即用。

## 核心特性

| 特性 | 说明 |
|------|------|
| **主芯片** | Nordic nRF52840 (ARM Cortex-M4, 64MHz, 1MB Flash, 256KB RAM) |
| **射频芯片** | Semtech SX1262 LoRa |
| **通信方式** | LoRa + BLE 5.0 |
| **温补晶振** | TCXO（提升频率稳定性与通信距离） |
| **发射功率** | 标准模组：最高 22 dBm（LoRa PA Boost） |
| **接收灵敏度** | -148 dBm（LoRa @ SF12, BW 125kHz） |
| **睡眠功耗** | 低至 2 µA（深度睡眠模式） |
| **供电电压** | 2.0 ~ 3.6 V |
| **工作温度** | -40°C ~ +85°C |
| **模块尺寸** | 约 20 × 30 mm |
| **接口** | UART / I2C / GPIO / USB / SWD |
| **固件** | 预装 Meshtastic，支持外接 1.3" TFT 显示屏、GPS、LED、蜂鸣器、按键、摇杆 |
| **兼容性** | 与 RAK4631 模组 IO 100% 兼容，可烧录 RAK4631-Arduino / RUI3 固件 |

## 支持频段

| 型号后缀 | 适用地区 | 频率范围 |
|----------|----------|----------|
| GAT562(L) | 中国 | CN470 |
| GAT562(L) | 欧洲 | EU433 |
| GAT562(H) | 欧洲 | EU868 |
| GAT562(H) | 北美 | US915 |
| GAT562(H) | 澳大利亚 | AU915 |
| GAT562(H) | 韩国 | KR920 |
| GAT562(H) | 亚洲 | AS923-1/2/3/4 |
| GAT562(H) | 印度 | IN865 |
| GAT562(H) | 俄罗斯 | RU864 |

> **提示**：购买时请确认型号（H = 高频段 / L = 低频段）符合您所在地区的无线电法规。

## 产品系列

GAT562 模组系列包括：

| 产品 | 描述 | 适用场景 |
|------|------|----------|
| **GAT562 Mesh Module** | 基础模组，22 dBm 发射功率 | 产品二次开发设计 |
| **GAT562 30S Mesh Module** | 增强模组，30 dBm 发射功率 | 远距离产品二次开发 |
| **GAT562 Mesh EVB Pro** | 开发板 | 快速验证与评估 |
| **GAT562 30S Board** | 30S 开发板 | 快速验证 30S 模组 |
| **GAT562 Mesh Tracker Pro** | 手持终端 | 便携使用 |
| **GAT562 30S Mesh Kit** | 30S 手持终端套装 | 强信号贴身设备 |
| **GAT562 Mesh Watch** | 手表形态终端 | 可穿戴场景 |
| **GAT562 Mesh Solar Relay** | 低成本太阳能中继 | 楼顶/户外固定中继 |
| **GAT562 Mesh Solar rakay Pro** | 高性能太阳能中继 | 强性能固定中继 |
| **GAT562 30S Mesh Solar rakay Pro** | 高功率太阳能中继 | 远距离固定中继 |

## 系统架构

```
┌─────────────────────────────────────┐
│         GAT562 Mesh Module          │
│  ┌───────────────┐  ┌────────────┐ │
│  │  nRF52840     │  │  SX1262    │ │
│  │  (MCU)        │◄─┤  (LoRa RF) │ │
│  │               │  │            │ │
│  │  64MHz ARM    │  │  TCXO      │ │
│  │  1MB Flash    │  │  22dBm     │ │
│  └───────┬───────┘  └──────┬─────┘ │
│          │                 │       │
│          │    BLE 5.0      │       │
│          │    LoRa         │       │
│          └───────┬─────────┘       │
│                  │                 │
│            I/O Port                │
│     (UART / I2C / GPIO / USB)      │
└─────────────────────────────────────┘
```

## 扩展外设支持

GAT562 Mesh Module 模组支持丰富的外部设备扩展：

- **显示屏**：1.3 英寸 TFT 屏幕（SPI 接口）
- **定位模块**：GPS 模块（串口连接）
- **输入设备**：按键、摇杆
- **指示输出**：LED 指示灯、蜂鸣器
- **无线连接**：蓝牙 5.0（近场配置与数据传输）
- **LoRa Mesh**：点对点、Mesh 网络自组网

## Mesh 网络优势

- **去中心化**：无单点故障，每个节点均可转发
- **长距离**：LoRa 穿透性强，支持数公里通信
- **离线通信**：无需互联网，手机无信号也能工作
- **低功耗**：nRF52 架构天然低功耗，待机持久
- **开源可定制**：Meshtastic 固件完全开源，支持二次开发
- **跨平台**：Android / iOS / Web 多端管理

## 与 RAK4631 的关系

GAT562 Mesh Module 基于与 RAK4631 相同的核心硬件平台（nRF52840 + SX1262），两者的主要区别：

| 对比项 | RAK4631 | GAT562 Mesh Module |
|--------|---------|-------------------|
| **核心硬件** | nRF52840 + SX1262 | nRF52840 + SX1262 |
| **IO 接口** | WisBlock 连接器 | WisBlock 连接器（兼容） |
| **官方固件** | RAK4631-Arduino / RUI3 | Meshtastic（预装） |
| **显示屏** | 需外接 | 内置 1.3" TFT 支持 |
| **GPS** | 需外接 | 支持内置/外接 |
| **封装** | WisBlock Core 模块 | 模组形态 |
| **RAK4631 固件** | 原生支持 | **完全兼容，可直接烧录** |

## 资源链接

- **Meshtastic 官方**：[https://meshtastic.org](https://meshtastic.org)
- **Meshtastic 固件**：[https://github.com/gat-iot/meshtastic_fw](https://github.com/gat-iot/meshtastic_fw)
- **GAT562 GitHub**：[https://github.com/gat-iot/GAT562-family](https://github.com/gat-iot/GAT562-family)
- **RAK4631 文档**：[RAK4631 WisBlock Core](/RAKWireless/rakwireless-docs/blob/master/docs/Product-Categories/WisBlock/RAK4631/README.md)

## 下一步

- [快速入门 →](./Quickstart/)  — 环境搭建与固件烧录
- [数据手册 →](./Datasheet/)  — 完整技术规格
