# Box for Root 配置

适用于 [Box for Root](https://github.com/boxproxy/box)，要求 sing-box `v1.14.0-alpha+`。

- `standard/`：普通代理模板
- `chain/`：机场节点 → 落地节点链式代理模板
- `prefer-ipv4.json`：IPv4 优先
- `prefer-ipv6.json`：IPv6 优先
- `no-preference.json`：不指定 IP 协议偏好

配置保留 `/data/adb/box` 日志路径以及 Box 使用的 TProxy/TUN 入站。使用前请通过 Sub-Store 填入真实节点，并修改 Clash API 密钥和端口。
