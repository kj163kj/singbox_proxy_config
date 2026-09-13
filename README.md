# SFI 配置

适用于 **sing-box for iOS（SFI）TestFlight 测试版**，要求核心版本为 `v1.15.0-alpha.3+`。

> [!IMPORTANT]
> 本分支配置只支持 SFI 测试版，不支持当前正式版/App Store 版。

## 配置文件

```text
standard/
├── only-ipv4.json
├── prefer-ipv4.json
├── prefer-ipv6.json
└── no-preference.json
chain/
├── only-ipv4.json
├── prefer-ipv4.json
├── prefer-ipv6.json
└── no-preference.json
```

- `standard`：普通代理模板
- `chain`：机场节点 → 落地节点的链式代理模板
- `only-ipv4`：DNS 仅使用 IPv4，拒绝 AAAA 查询，TUN 仅保留 IPv4 地址
- `prefer-ipv4`：IPv4 优先
- `prefer-ipv6`：IPv6 优先
- `no-preference`：不指定 IP 协议偏好

## 使用说明

这些文件是 Sub-Store 模板，需先填入真实节点，再将生成的最终配置导入 SFI 测试版。未渲染模板不能直接启动。
????? sing-box ?? TUN TCP/IP ?????????????? `stack` ??????????????? `v1.15.0-alpha.3` ??????
