# SFI 配置

适用于 **sing-box for iOS（SFI）** 普通 App Store/TestFlight 版，要求 sing-box `v1.14.0-alpha+`。

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

- `standard`：普通代理模板，没有机场前置节点
- `chain`：链式代理模板，通过“机场节点 → 落地节点”连接
- `prefer-ipv4`：DNS 优先使用 IPv4
- `prefer-ipv6`：DNS 优先使用 IPv6
- `no-preference`：不指定 DNS IP 协议偏好

> [!NOTE]
> 这些文件是 Sub-Store 配置模板，部分 selector 的 `outbounds` 需要在订阅转换时填入真实节点。未渲染模板不能直接启动。

## SFI 平台适配

这些配置已经针对 Apple NetworkExtension 调整：

- 删除 Linux/Android 专用的 TUN `auto_redirect`
- 删除 SFI 未实现的 `strict_route`
- 删除由 Darwin 管理的固定 `interface_name`
- 删除 iOS 不支持的 UID/包名筛选字段
- 保留双栈 TUN 地址与 `auto_route: true`
- 使用 `stack: mixed` 和 `dns_mode: hijack`
- 将 `udp_nat_max` 限制为 iOS 默认的 `4096`
- 删除固定日志输出路径，日志请在 SFI 的 Service Log 中查看
- 删除 Clash API，使用 SFI 自带 Dashboard 管理模式、连接和策略组

## 使用方法

1. 选择普通模板或链式代理模板；
2. 选择 IPv4 优先、IPv6 优先或不指定协议偏好；
3. 使用 Sub-Store 填入节点并生成最终配置；
4. 将最终配置作为本地或远程 Profile 导入 SFI；
5. 启动前确认 SFI 核心版本为 `v1.14.0-alpha+`。

SFI 远程配置也可以通过 URL Scheme 导入：

```text
sing-box://import-remote-profile?url=URL编码后的配置地址#URL编码后的名称
```

## 平台限制

普通 SFI 不支持以下匹配字段：

- `process_name`
- `process_path`
- `process_path_regex`
- `user` / `user_id`
- Android `package_name`

进程及用户匹配仅在越狱版 SFI 中可用。

## 校验

六份模板的诊断副本均已使用 sing-box `1.14.0-alpha.48` 检查通过。正式模板保留空 selector，等待 Sub-Store 填入真实节点。
