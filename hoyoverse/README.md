# HoYoverse International (OS) — Surge Proxy Rules

原神 / 崩坏：星穹铁道 / 绝区零 / 崩坏 3 **国际服** 的游戏下载、更新与游戏连接代理规则，参考 [Genshin.module](https://cdn.jsdelivr.net/gh/scalpelliu/surge_ios-rule@main/module/Genshin.module) 风格改写。

---

## 核心规则

```
IP-ASN + DEST-PORT 复合匹配
```

| 游戏 | 端口 (UDP) | 服务器 ASN |
|------|:-----------:|-----------|
| 原神 (Genshin Impact) | **22101/22102** | AS45102 (阿里云) / AS16509+14618 (AWS) |
| 星穹铁道 (HSR) | **23301** | AS45102 (阿里云) / AS16509+14618 (AWS) |
| 绝区零 (ZZZ) | **20501** | AS45102 (阿里云) / AS16509+14618 (AWS) |

---

## 使用方法

### 方式一：仅代理游戏更新下载（推荐）

Surge → **模块** → **安装新模块**：

```
https://raw.githubusercontent.com/scalpl/surge_ios-rule/main/module/Hoyoverse_Download.sgmodule
```

此模块包含 HoYoPlay 包清单接口，以及原神、崩坏：星穹铁道、绝区零和崩坏 3 国际服的更新包 CDN。不会代理游戏服务器连接。

### 方式二：下载与游戏连接全量模块

Surge → **模块** → **安装新模块**：

```
https://raw.githubusercontent.com/scalpl/surge_ios-rule/main/module/Hoyoverse_All.sgmodule
```

全量模块包含与下载模块相同的 HoYoPlay/更新 CDN 规则，并加入三款游戏的 `IP-ASN + DEST-PORT` 连接规则。

### 方式三：引用规则集

```ini
[Rule]
# HoYoPlay 与游戏更新包下载
RULE-SET,"/path/Hoyoverse_Download.list",HOYOVERSE

# IP-ASN + 端口复合规则（精确，推荐）
RULE-SET,"/path/Hoyoverse_IP.list",HOYOVERSE

# 或仅端口规则（兼容）
RULE-SET,"/path/Hoyoverse_Ports.list",HOYOVERSE

# 域名辅助规则（登录/API/SDK）
RULE-SET,"/path/Hoyoverse_Common.list",HOYOVERSE
RULE-SET,"/path/Hoyoverse_Genshin.list",HOYOVERSE
RULE-SET,"/path/Hoyoverse_StarRail.list",HOYOVERSE
RULE-SET,"/path/Hoyoverse_Zenless.list",HOYOVERSE
```

> `HOYOVERSE` 策略 → 指向你的海外代理节点。

---

## 文件结构

```
hoyoverse/
├── Hoyoverse_Download.list ← HoYoPlay 与游戏更新包下载域名
├── Hoyoverse_IP.list       ← IP-ASN + 端口复合规则
├── Hoyoverse_Ports.list    ← 仅端口规则（兼容）
├── Hoyoverse_Common.list   ← 通用域名
├── Hoyoverse_Genshin.list  ← 原神域名
├── Hoyoverse_StarRail.list ← 星穹铁道域名
├── Hoyoverse_Zenless.list  ← 绝区零域名
├── Hoyoverse_Cloud.list    ← 云游戏域名
└── README.md

module/
├── Hoyoverse_Download.sgmodule ← 仅更新下载模块
└── Hoyoverse_All.sgmodule      ← 更新下载 + 游戏连接全量模块
```

---

## License

MIT
