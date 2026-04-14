# GAT562 Mesh EVB Pro

## 产品简介

GAT562 Mesh EVB Pro 是一款基于 **GAT562 Mesh Module** 的多功能开发评估板，板载 GAT562 模组核心，引出全部 IO 引脚，预装 Meshtastic 固件，适合快速功能验证、产品评估和二次开发。

## 硬件特性

| 特性 | 说明 |
|------|------|
| **核心模组** | GAT562 Mesh Module（nRF52840 + SX1262 + TCXO） |
| **发射功率** | 最高 22 dBm（LoRa PA Boost） |
| **供电方式** | USB Type-C / DC Jack / 电池接口 |
| **调试接口** | 原生 USB（烧录 + 调试）/ SWD 接口 |
| **显示接口** | 预留 1.3" TFT 屏幕接口 |
| **GPS 接口** | 预留 GPS 模块接口（UART） |
| **IO 扩展** | 全部引脚通过排针引出（兼容 RAK5005-O） |
| **板载外设** | LED × 2 / 按键 × 2 / 复位键 |
| **尺寸** | 约 85 × 60 mm |

## IO 引脚图

> 完整 IO 引脚定义图：[GAT562 Mesh EVB PRO IO.png](https://github.com/gat-iot/GAT562-family/blob/main/GAT562%20Mesh%20EVB%20PRO%20IO.png)

## 快速入门

### 步骤 1：连接设备

1. 用 USB-C 数据线连接 EVB Pro 到电脑
2. 蓝色 LED 亮起表示开机正常
3. 在电脑上识别到 USB 串口（COMx）

### 步骤 2：配置 Meshtastic

1. 手机安装 Meshtastic App
2. 打开 App，搜索 BLE 设备
3. 连接后配置频道、节点名称

### 步骤 3：烧录固件

- **Web Flasher**：[meshtastic.org/flasher](https://meshtastic.org/flasher)，选择 RAK4631
- **Arduino IDE**：选择 `WisBlock Core → RAK4631` 开发板

## 扩展接口

| 接口 | 说明 |
|------|------|
| **Slot A / B / C / D** | WisBlock 兼容传感器扩展槽 |
| **IO 排针** | 全部 GPIO 引出 |
| **USB** | 烧录 / 供电 / 串口调试 |
| **SWD** | JTAG / SWD 调试 |
| **GPS 接口** | 串口连接 GPS 模块 |
| **TFT 屏幕** | SPI 接口 1.3" 屏幕 |

## 相关文档

- [GAT562 Mesh Module 数据手册 →](../GAT562-Mesh-Module/Datasheet/)
- [快速入门 →](../GAT562-Mesh-Module/Quickstart/)
- [GitHub 资源](https://github.com/gat-iot/GAT562-family)
