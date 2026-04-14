# GAT562 Mesh Module 数据手册

## 硬件规格

### 芯片组合

| 器件 | 型号 | 厂商 | 说明 |
|------|------|------|------|
| MCU | nRF52840 | Nordic Semiconductor | ARM Cortex-M4, 64MHz, 1MB Flash, 256KB RAM |
| LoRa RF | SX1262 | Semtech | 支持 LoRa / LoRaWAN |
| 温补晶振 | TCXO | — | 提升 LoRa 频率稳定性 |

### 尺寸与封装

| 参数 | 值 |
|------|-----|
| 模块尺寸 | 约 20 × 30 mm |
| 安装孔距 | 兼容 RAK5005-O 底板 |
| 连接器 | WisBlock 标准连接器（兼容 RAK4631） |

### 供电规格

| 符号 | 描述 | 最小 | 典型 | 最大 | 单位 |
|------|------|------|------|------|------|
| VDD | MCU 供电电压 | 2.0 | 3.3 | 3.6 | V |
| VBAT_SX | SX1262 供电电压 | 2.0 | 3.3 | 3.7 | V |
| VBUS | USB 供电电压 | 4.35 | 5.0 | 5.5 | V |
| VBAT_NRF | nRF52840 高压电源 | 2.5 | — | 5.5 | V |

### 功耗特性

| 模式 | 电流 | 条件 |
|------|------|------|
| 深度睡眠 | **2.0 µA** | LoRa + BT 均关闭 |
| 接收 (LoRa) | 17 mA | LoRa 接收模式，BT 休眠 |
| 接收 (BLE) | 11.5 mA | BLE 2Mbps 接收模式，LoRa 休眠 |
| 发射 LoRa @17 dBm | 92 mA | PA Boost 模式 |
| 发射 LoRa @20 dBm | 125 mA | PA Boost + BT 休眠 |
| 发射 BLE @4 dBm | 9 mA | BLE 发射，LoRa 休眠 |

### LoRa 射频规格

| 参数 | 值 |
|------|-----|
| 频率范围 | 150 ~ 960 MHz（依型号 H/L） |
| 带宽 | 7.8 kHz ~ 500 kHz |
| 发射功率 | +22 dBm（PA Boost 模式） |
| 接收灵敏度 | -148 dBm（SF12, BW 125kHz） |
| 扩频因子 | SF5 ~ SF12 |
| 编码率 | 4/5, 4/6, 4/7, 4/8 |
| 前导码 | 可编程，6 ~ 65535 符号 |

### BLE 射频规格

| 参数 | 值 |
|------|-----|
| 标准 | Bluetooth 5.0 LE |
| 发射功率 | -20 dBm ~ +4 dBm（4 dB 步进） |
| 接收灵敏度 | -96 dBm（1 Mbps LE） |
| 工作频率 | 2.400 ~ 2.4835 GHz |

### 环境规格

| 参数 | 值 |
|------|-----|
| 工作温度 | -40°C ~ +85°C |
| 存储温度 | -40°C ~ +85°C |
| 湿度 | 5% ~ 95% RH（非凝结） |
| ESD | ±2 kV（HBM） |

### IO 接口定义（RAK4631 兼容）

GAT562 Mesh Module 的 WisConnector 引脚定义与 RAK4631 完全兼容：

| 引脚 | 功能 | 描述 |
|------|------|------|
| 1 | GND | 电源地 |
| 2 | VDD | 3.3V 供电 |
| 3 | USB_P | USB D+ |
| 4 | USB_N | USB D- |
| 5 | SWDIO | SWD 调试数据 |
| 6 | SWDCLK | SWD 调试时钟 |
| 7 | RST | 复位 |
| 8 | NFC1 | NFC 接口 1（可选） |
| 9 | NFC2 | NFC 接口 2（可选） |
| 10 | UART1_TX | 串口 1 发送 |
| 11 | UART1_RX | 串口 1 接收 |
| 12 | I2C_SDA | I2C 数据 |
| 13 | I2C_SCL | I2C 时钟 |
| 14 | GPIO1 (WB_IO1) | 通用 IO 1 |
| 15 | GPIO2 (WB_IO2) | 通用 IO 2（可控制 3.3V 电源） |
| 16 | AIN (WB_A0) | 模拟输入 |
| 17 | LED_GREEN | 绿色 LED |
| 18 | LED_BLUE | 蓝色 LED |
| — | — | — |
| A槽 | UART1 / I2C | WisBlock Slot A |
| B槽 | UART1 / I2C | WisBlock Slot B |
| C槽 | UART1 / I2C | WisBlock Slot C |
| D槽 | UART1 / I2C | WisBlock Slot D |

> **注**：UART2 仅在 WisBlock IO 槽可用。I2C_2 仅在 WisBlock IO 槽可用。

### 固件烧录接口

| 接口 | 描述 |
|------|------|
| **原生 USB** | Serial DFU 烧录（通过 Arduino IDE / nrfutil） |
| **SWD** | Serial Wire Debug（需要 J-Link / nRF-Dongle） |
| **OTA** | 无线固件更新（通过 Meshtastic App） |
| **蓝牙** | BLE OTA（通过 Meshtastic App） |

### 支持的固件

| 固件 | 描述 | 来源 |
|------|------|------|
| **Meshtastic** | 预装，Mesh 网络通信 | 内置 |
| **RAK4631 Arduino BSP** | Arduino 生态，WisBlock 库支持 | 可直接烧录 |
| **RAK4631-R RUI3** | RAK 官方 AT 命令固件 | 可直接烧录 |
| **自定义固件** | nRF5 SDK / Zephyr RTOS | 用户自行开发 |

### 认证（参考 RAK4631 同款模组）

| 认证 | 状态 |
|------|------|
| CE | ✅ |
| FCC | ✅ |
| ISED | ✅ |
| KCC | ✅ |
| RCM | ✅ |
| REACH | ✅ |
| RoHS | ✅ |

> 认证信息由 RAK4630/RAK4631 同款核心模组延伸，GAT562 具体认证请参考产品出货批次。

### 原理图与封装文件

GAT562 硬件设计文件（来源：gat-iot/GAT562-family GitHub 仓库）：

| 文件 | 说明 | 下载 |
|------|------|------|
| GAT562 30S Mesh Module 封装定义.pdf | 模组封装尺寸与焊盘定义 | [GitHub](https://github.com/gat-iot/GAT562-family/blob/main/GAT562%2030S%20Mesh%20Module%E5%B0%81%E8%A3%85%E5%AE%9A%E4%B9%89.pdf) |
| GAT562 30S Mesh KIT V1.1 SCH.pdf | 30S 开发板原理图 | [GitHub](https://github.com/gat-iot/GAT562-family/blob/main/GAT562%2030S%20Mesh%20KIT%20V1.1%20SCH.pdf) |
| GAT562 Mesh EVB PRO IO.png | 开发板 IO 引脚图 | [GitHub](https://github.com/gat-iot/GAT562-family/blob/main/GAT562%20Mesh%20EVB%20PRO%20IO.png) |

---

## 相关文档

- [GAT562 Mesh Module 概述](./)
- [快速入门 →](../Quickstart/)
