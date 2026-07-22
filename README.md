# SFL 配置

适用于官方 **sing-box for Linux (SFL)**，要求核心版本为 `v1.14.0-alpha.50+`。

> [!IMPORTANT]
> Linux GUI 支持从 sing-box `1.14.0-alpha.48` 开始。本分支配置按当前最新版 `1.14.0-alpha.50` 适配并校验，请使用最新版 SFL。

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

这些文件是 Sub-Store 模板，需先填入真实节点，再将生成的最终配置作为本地或远程 Profile 导入 SFL。未渲染模板不能直接启动。

官方 Linux GUI 由系统服务运行核心。请使用官方安装包完成 daemon、systemd 和权限配置，不要只复制 GUI 可执行文件。
