# HoYoverse International (OS) — Surge Proxy Rules

原神 / 崩坏：星穹铁道 / 绝区零 **国际服** 代理规则，参考 [Genshin.module](https://cdn.jsdelivr.net/gh/scalpelliu/surge_ios-rule@main/module/Genshin.module) 风格改写。

---

## 核心规则

```
IP-ASN + DEST-PORT 复合匹配
```

| 游戏 | 端口 (UDP) | 服务器 ASN |
|------|:-----------:|-----------|
| 原神 (Genshin Impact) | **22102** | AS45102 (阿里云) / AS16509+14618 (AWS) |
| 星穹铁道 (HSR) | **23301** | AS45102 (阿里云) / AS16509+14618 (AWS) |
| 绝区零 (ZZZ) | **20501** | AS45102 (阿里云) / AS16509+14618 (AWS) |

---

## 使用方法

### 方式一：Module（推荐）

Surge → **模块** → **安装新模块**：

```
https://raw.githubusercontent.com/scalpl/surge_ios-rule/main/module/Hoyoverse_All.sgmodule
```

模块内容：

```
#!name= HoYoverse International (OS)
[Rule]
# Genshin Impact OS: Alibaba AS45102 + AWS + port 22102
OR,((AND,((IP-ASN,45102,no-resolve),(DEST-PORT,22102))),(AND,((IP-ASN,16509,no-resolve),(DEST-PORT,22102))),(AND,((IP-ASN,14618,no-resolve),(DEST-PORT,22102)))),HOYOVERSE
# Honkai: Star Rail OS: Alibaba AS45102 + AWS + port 23301
OR,((AND,((IP-ASN,45102,no-resolve),(DEST-PORT,23301))),(AND,((IP-ASN,16509,no-resolve),(DEST-PORT,23301))),(AND,((IP-ASN,14618,no-resolve),(DEST-PORT,23301)))),HOYOVERSE
# Zenless Zone Zero OS: Alibaba AS45102 + AWS + port 20501
OR,((AND,((IP-ASN,45102,no-resolve),(DEST-PORT,20501))),(AND,((IP-ASN,16509,no-resolve),(DEST-PORT,20501))),(AND,((IP-ASN,14618,no-resolve),(DEST-PORT,20501)))),HOYOVERSE
```

### 方式二：引用规则集

```ini
[Rule]
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
├── Hoyoverse_All.sgmodule  ← 主模块（3 行 IP-ASN + 端口复合规则）
├── Hoyoverse_IP.list       ← IP-ASN + 端口复合规则
├── Hoyoverse_Ports.list    ← 仅端口规则（兼容）
├── Hoyoverse_Common.list   ← 通用域名
├── Hoyoverse_Genshin.list  ← 原神域名
├── Hoyoverse_StarRail.list ← 星穹铁道域名
├── Hoyoverse_Zenless.list  ← 绝区零域名
├── Hoyoverse_Cloud.list    ← 云游戏域名
└── README.md
```

---

## License

MIT
