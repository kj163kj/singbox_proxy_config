# OpenWrt-momo 配置

适用于 [OpenWrt-momo](https://github.com/nikkinikki-org/OpenWrt-momo)，配置字段按 sing-box `v1.14.0-alpha+` 编写。

- `standard/`：普通代理模板
- `chain/`：机场节点 → 落地节点链式代理模板
- `prefer-ipv4.json`：IPv4 优先
- `prefer-ipv6.json`：IPv6 优先
- `no-preference.json`：不指定 IP 协议偏好

配置包含 Momo 默认约定的 `dns-in`、`redirect-in`、`tproxy-in`、`tun-in` 和 `fake-ip-dns-server` 标签。Momo 根据这些标签读取端口和接口并生成 fw4/路由规则，除非同步修改 UCI，否则不要改名。

Momo 会通过配置混入注入 Clash API。请在 Momo 的“外部控制”设置中修改监听端口和密钥，不要把真实密钥写进公开配置。
