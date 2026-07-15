# Surge iOS Rules

Surge modules and rule sets for routing HoYoverse international (OS) game traffic through a dedicated proxy policy.

The repository covers HoYoPlay downloads and selected connections for Genshin Impact, Honkai: Star Rail, Zenless Zone Zero, and Honkai Impact 3rd.

## Quick Start

In Surge, open **Modules**, choose **Install Module from URL**, and install one of the following modules:

| Module | Purpose | URL |
| --- | --- | --- |
| Update downloads (recommended) | Proxies HoYoPlay metadata and game update packages without routing game-server connections | [`Hoyoverse_Download.sgmodule`](https://raw.githubusercontent.com/scalpl/surge_ios-rule/main/module/Hoyoverse_Download.sgmodule) |
| Complete rules | Proxies update downloads and selected game-server connections | [`Hoyoverse_All.sgmodule`](https://raw.githubusercontent.com/scalpl/surge_ios-rule/main/module/Hoyoverse_All.sgmodule) |

Both modules expect a Surge policy named `HOYOVERSE`. Create that policy and point it to the overseas proxy or policy group you want to use.

## Game Connection Rules

The complete module combines destination ports with cloud-provider ASNs to reduce unintended matches:

| Game | Destination port | ASN |
| --- | --- | --- |
| Genshin Impact | `22101`, `22102` | AS45102 (Alibaba Cloud), AS16509 and AS14618 (AWS) |
| Honkai: Star Rail | `23301` | AS45102 (Alibaba Cloud), AS16509 and AS14618 (AWS) |
| Zenless Zone Zero | `20501` | AS45102 (Alibaba Cloud), AS16509 and AS14618 (AWS) |

The download rules also cover HoYoPlay package metadata and update CDNs for Genshin Impact, Honkai: Star Rail, Zenless Zone Zero, and the international variants of Honkai Impact 3rd.

## Rule Sets

Use the individual files in [`hoyoverse/`](hoyoverse/) when you need more control than the ready-to-install modules provide.

| Rule set | Contents |
| --- | --- |
| [`Hoyoverse_Download.list`](hoyoverse/Hoyoverse_Download.list) | HoYoPlay metadata and game update downloads |
| [`Hoyoverse_IP.list`](hoyoverse/Hoyoverse_IP.list) | Precise ASN and destination-port combinations |
| [`Hoyoverse_Ports.list`](hoyoverse/Hoyoverse_Ports.list) | Destination-port-only compatibility rules |
| [`Hoyoverse_Common.list`](hoyoverse/Hoyoverse_Common.list) | Shared account, API, SDK, and community domains |
| [`Hoyoverse_Genshin.list`](hoyoverse/Hoyoverse_Genshin.list) | Genshin Impact domains |
| [`Hoyoverse_StarRail.list`](hoyoverse/Hoyoverse_StarRail.list) | Honkai: Star Rail domains |
| [`Hoyoverse_Zenless.list`](hoyoverse/Hoyoverse_Zenless.list) | Zenless Zone Zero domains |
| [`Hoyoverse_Cloud.list`](hoyoverse/Hoyoverse_Cloud.list) | HoYoverse cloud-gaming domains |

For example:

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/scalpl/surge_ios-rule/main/hoyoverse/Hoyoverse_Download.list,HOYOVERSE
RULE-SET,https://raw.githubusercontent.com/scalpl/surge_ios-rule/main/hoyoverse/Hoyoverse_IP.list,HOYOVERSE
```

Use `Hoyoverse_Ports.list` instead of `Hoyoverse_IP.list` only when your Surge version does not support the combined rules. Port-only matching is less precise.

## Legacy Genshin Module

[`module/Genshin.module`](module/Genshin.module) is retained for the original Genshin Impact Asia-server setup. It matches AS45102 on ports `22101` and `22102` and expects a policy named `🇯🇵 Japan`.

For new configurations, prefer one of the HoYoverse modules above.

## Notes

- These rules target HoYoverse international servers and may not apply to mainland China servers.
- Service domains, network providers, and ports can change. Review and update the rules if traffic stops matching.
- This is an independent community project and is not affiliated with or endorsed by HoYoverse or Surge Networks.

## License

This project is available under the [MIT License](LICENSE).
