# SFA / SFW 配置

适用于 sing-box for Android（SFA）和 sing-box for Windows（SFW），要求 sing-box `v1.14.0-alpha+`。

- `standard/`：普通代理模板
- `chain/`：机场节点 → 落地节点链式代理模板
- `prefer-ipv4.json`：IPv4 优先
- `prefer-ipv6.json`：IPv6 优先
- `no-preference.json`：不指定 IP 协议偏好

使用前请通过 Sub-Store 填入真实节点，并将 Clash API 的 `secret` 和监听端口改为你自己的值。不要将真实密钥提交到公开仓库。
