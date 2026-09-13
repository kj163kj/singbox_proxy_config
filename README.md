# SFA / SFW 配置

适用于 sing-box for Android（SFA）和 sing-box for Windows（SFW），要求 sing-box `v1.14.0-alpha+`。

- `standard/`：普通代理模板
- `chain/`：机场节点 → 落地节点链式代理模板
- `only-ipv4.json`：DNS 仅使用 IPv4，拒绝 AAAA 查询，TUN 仅保留 IPv4 地址
- `prefer-ipv4.json`：IPv4 优先
- `prefer-ipv6.json`：IPv6 优先
- `no-preference.json`：不指定 IP 协议偏好

所有模板均包含 TUN 和 [mixed 入站](https://sing-box.sagernet.org/configuration/inbound/mixed/)。mixed 监听 `127.0.0.1:2080`，支持 HTTP 和 SOCKS4/4a/5，无需认证；应用可将代理地址设为该地址。`set_system_proxy` 为 `false`，如需使用系统代理，请手动配置。

使用前请通过 Sub-Store 填入真实节点，并将 Clash API 的 `secret` 和监听端口改为你自己的值。不要将真实密钥提交到公开仓库。
