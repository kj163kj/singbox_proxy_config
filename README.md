# SFM 配置

适用于 **sing-box for macOS（SFM）**，要求核心版本为 `v1.14.0-alpha+`。

> [!WARNING]
> 本分支配置尚未经 macOS 实机测试。如遇到兼容性或运行问题，请通过仓库 [Issues](https://github.com/kj163kj/singbox_proxy_config/issues) 反馈，并附上 SFM 版本、macOS 版本和相关日志。

## 配置文件

```text
standard/
├── prefer-ipv4.json
├── prefer-ipv6.json
└── no-preference.json
chain/
├── prefer-ipv4.json
├── prefer-ipv6.json
└── no-preference.json
```

- `standard`：普通代理模板
- `chain`：机场节点 → 落地节点的链式代理模板
- `prefer-ipv4`：IPv4 优先
- `prefer-ipv6`：IPv6 优先
- `no-preference`：不指定 IP 协议偏好

## 使用说明

这些文件是 Sub-Store 模板，需先填入真实节点，再将生成的最终配置导入 SFM。未渲染模板不能直接启动。
