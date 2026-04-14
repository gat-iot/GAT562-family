# GAT562 Mesh Module 快速入门

## 准备工作

### 所需物品

| 物品 | 说明 |
|------|------|
| **GAT562 Mesh Module** | 模组本体 |
| **GAT562 Mesh EVB Pro** 或 **RAK5005-O** | 开发底板（提供 USB / 供电 / 引脚扩展） |
| **USB 数据线** | USB Type-A to Type-C（建议 3.0 线缆） |
| **Meshtastic App** | Android / iOS 应用（配置和管理设备） |
| **电脑（可选）** | 如需烧录 Arduino / RUI3 固件 |

### 软件准备

#### Meshtastic 固件（预装，开箱即用）

GAT562 Mesh Module 出厂已预装 Meshtastic 固件，支持以下方式更新：

1. **蓝牙 OTA（推荐）**
   - 在手机上安装 [Meshtastic App](https://meshtastic.org/)
   - 打开 App，搜索附近设备
   - 点击设备 → 设置 → 检查固件更新

2. **USB 线刷**
   - 通过 Web Flash 工具：[flasher.meshtastic.org](https://flasher.meshtastic.org)
   - 选择 `RAK4631` 作为目标设备（IO 兼容）
   - 选择对应频段，连接设备后点击 Flash

#### Arduino IDE 开发（烧录 RAK4631 固件）

> GAT562 Mesh Module **IO 与 RAK4631 完全兼容**，可直接参考 RAK4631 的 Arduino 开发流程。

1. 下载并安装 [Arduino IDE](https://www.arduino.cc/en/Main/Software)
2. 添加 WisBlock 板级支持包（BSP）：
   - 打开 Arduino IDE → 文件 → 首选项 → 附加开发板管理器网址
   - 添加：`https://raw.githubusercontent.com/RAKWireless/RAKwireless-Arduino-BSP-Index/main/package_rakwireless.com_wise模块_index.json`
   - 打开 工具 → 开发板 → 开发板管理器，搜索 `WisBlock`，安装
3. 选择开发板：**Tools → Board → WisBlock Core → RAK4631**
4. 上传示例代码

#### PlatformIO 开发

参考 [PlatformIO + RAK4631 完整配置指南](https://docs.rakwireless.com/Knowledge-Hub/Learn/Board-Support-Package-Installation-in-PlatformIO/)

---

## 硬件连接

### 安装到底板

将 GAT562 Mesh Module 对准 RAK5005-O（或 GAT562 Mesh EVB Pro）的 WisBlock 插槽，**缺口对缺口**，垂直轻轻按压直至两侧卡扣卡紧。

```
  WisBlock Slot
  ┌─────────────────┐
  │  [CONN A] [CONN B]  │
  │  [CONN C] [CONN D]  │
  │  [   USB-C    ]  │
  └─────────────────┘
       ↑ 缺口对齐
  ┌─────────────────┐
  │                 │
  │   GAT562 Module │  ← 安装在此
  │    (MCU+LoRa)   │
  │                 │
  └─────────────────┘
```

### LED 指示说明

| LED | 颜色 | 说明 |
|-----|------|------|
| 电源 | 红色（底板） | 常亮 = 供电正常 |
| 运行 | 绿色 / 蓝色 | 闪烁 = 系统运行中 |
| LoRa | — | — |
| BLE | — | — |

---

## Meshtastic 基础配置

### 首次开机

1. 给设备供电（USB 或电池）
2. 设备自动开机，蓝色 LED 闪烁
3. 手机打开 Meshtastic App
4. App 自动搜索并连接 BLE
5. 设置节点名称和频道配置

### 关键参数配置

| 参数 | 说明 | 建议值 |
|------|------|--------|
| 节点名称 | 设备昵称 | 例如 "Node-001" |
| 频道 | Mesh 通信频道 | 默认 `LongFast`（公开频道） |
| 地理定位 | GPS 位置共享 | 开启 |
| 加密 | 防止窃听 | 默认 AES256 |
| 功率 | LoRa 发射功率 | 默认 20 dBm |
| 扩频因子 | 距离与速率平衡 | SF7（默认）/ SF10（远距离） |
| 跳频 | 中继转发 | 开启 |

### LoRa 参数对照表

| 模式 | 扩频因子 | 带宽 | 典型距离 | 适用场景 |
|------|----------|------|----------|----------|
| Short | SF7 | 500 kHz | ~1-3 km | 城市密集区 |
| Medium | SF9 | 250 kHz | ~3-8 km | 郊区 |
| Long | SF10 | 125 kHz | ~8-15 km | 开阔地 |
| Very Long | SF12 | 62.5 kHz | ~15 km+ | 超远距离 |

---

## 固件烧录（进阶）

### 烧录 Meshtastic 固件（通过 USB + Web Flasher）

1. 访问 [meshtastic.org/flasher](https://meshtastic.org/flasher)
2. 选择平台：**Statically compiled for RAK4631**
3. 选择固件版本和频段
4. 用 USB 连接设备
5. 点击 **Flash** 按钮

### 烧录 RAK4631 Arduino BSP 固件

```bash
# 使用 nrfutil（ Nordic 官方工具）
nrfutil dfu usb-serial \
  --package <firmware.zip> \
  --serial-port COMx
```

### 烧录 RUI3 固件（RAK4631-R 模式）

GAT562 可转换为 RAK4631-R 固件模式（基于 RUI3 AT 命令）：

1. 参考 [RAK4631-R DFU 升级指南](https://docs.rakwireless.com/Product-Categories/WisBlock/RAK4631-R/DFU/)
2. 下载 RUI3 固件
3. 通过 USB 串口烧录

---

## IO 引脚使用（参考 RAK4631）

### WisBlock 标准 IO 映射

在 Arduino IDE / PlatformIO 中，GAT562 Mesh Module 的 IO 映射与 RAK4631 完全一致：

```cpp
// WisBlock 标准 IO 映射（GAT562 = RAK4631）
#define WB_IO1   2   // GPIO2，数字 IO
#define WB_IO2   3   // GPIO3，可控制 3.3V 电源（低功耗传感器的使能脚）
#define WB_IO3   29  // GPIO4
#define WB_IO4   28  // GPIO5
#define WB_IO5   11  // GPIO6
#define WB_A0    4    // ADC 模拟输入

// 板载 LED
#define LED_GREEN 37  // 绿色 LED（高电平点亮）
#define LED_BLUE  38  // 蓝色 LED（高电平点亮）

// 串口
#define Serial1   UART1   // 连接 Slot A / IO 槽
#define Serial2   UART2   // 仅 IO 槽可用
```

### I2C 总线

```cpp
// I2C_1（默认，Slots A-D + 扩展排针）
Wire.begin();

// I2C_2（仅 IO 槽可用）
TwoWire Wire2(1);
Wire2.begin();
```

### 低功耗示例

```cpp
#include <rtl8720du.hpp>

void setup() {
  // 初始化
}

void loop() {
  // 发送数据
  // ...

  // 进入深度睡眠（功耗 ~2 µA）
  sd_power_system_off();
}

void enterSleep() {
  // 关闭 LoRa 和 BLE
  // 配置 WB_IO2 控制外部传感器断电
  pinMode(WB_IO2, OUTPUT);
  digitalWrite(WB_IO2, LOW);  // 关闭 3.3V 电源
  delay(100);
  sd_power_system_off();
}
```

---

## 常见问题

**Q: GAT562 能用 RAK4631 的固件吗？**
A: 可以。GAT562 IO 与 RAK4631 完全兼容，Arduino、RUI3、Meshtastic 固件均可直接烧录使用。

**Q: 固件更新后数据会丢失吗？**
A: 使用 Meshtastic OTA 或 DFU 升级不会丢失节点配置（配置存储在 Flash 分区）。完整擦除后需重新配置。

**Q: 如何进入 bootloader 模式？**
A: 在开机状态下快速双击复位键，设备进入 DFU 模式，蓝色 LED 快闪。

**Q: GPS 模块如何连接？**
A: GPS 模块通过 UART1 连接（TX→RX，RX→TX），或使用 Slot A 连接座。Meshtastic App 可自动识别 GPS 数据。

**Q: 30 dBm 版本（GAT562 30S）和标准版有什么差异？**
A: 30S 版本使用外置 PA，LoRa 发射功率提升至 30 dBm，适合超远距离通信场景。其他 IO 完全一致。

---

## 相关文档

- [GAT562 Mesh Module 概述 →](./)
- [数据手册 →](../Datasheet/)
- [Meshtastic 官方文档](https://meshtastic.org/docs/)
- [RAK4631 Arduino BSP](https://github.com/RAKWireless/RAKwireless-Arduino-BSP-Index)
- [WisBlock 示例代码](https://github.com/RAKWireless/WisBlock/tree/master/examples)
