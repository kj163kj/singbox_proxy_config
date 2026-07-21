# iOS / SFI 适配结论

目标客户端：sing-box for iOS（SFI）普通 App Store/TestFlight 版，基于 Apple NetworkExtension。

## 相对 SFA/SFW 必须修改

1. 删除 TUN `auto_redirect`
   - 这是 Linux/Android 路由加速功能；非 Linux 的 sing-tun 实现返回 `invalid argument`。
2. 删除 TUN `strict_route`
   - SFI 官方功能表明确标注未实现。
3. 删除 `interface_name`
   - SFI 的 utun 接口名称由 Darwin/NetworkExtension 管理。
4. 删除 `include_uid` / `exclude_uid`、包名筛选
   - iOS NetworkExtension 不支持 Android UID/包名路由。
5. 删除 Clash API
   - SFI 自带 Dashboard/命令服务器，可直接切换 Mode 和 selector；额外监听 Clash API 没必要，还增加暴露面和内存开销。
6. 不写日志 `output`
   - SFI 服务日志在 App 的 Settings → View Service Log 查看，不能使用 Box/OpenWrt 的固定文件路径。

## 建议设置

```json
{
  "type": "tun",
  "tag": "tun-in",
  "address": [
    "172.18.0.1/30",
    "fdfe:dcba:9876::1/126"
  ],
  "mtu": 1420,
  "stack": "mixed",
  "dns_mode": "hijack",
  "auto_route": true,
  "udp_nat_max": 4096
}
```

- `mixed` 是启用 gVisor 构建时的默认栈，兼顾 system TCP 与 gVisor UDP。
- iOS 上 `udp_nat_max` 默认本来就是 4096；显式写出仅用于说明和限制资源。
- `auto_route` 必须保留，SFI 用它建立 NEIPv4/NEIPv6 路由和 DNS 设置。
- 双栈 `address` 应保留，否则 IPv6 优先模板缺少完整的 IPv6 TUN 通道。

## iOS 规则限制

普通 SFI 不支持：

- `process_name`
- `process_path`
- `user` / `user_id`
- Android `package_name`

只有越狱版 SFI 才支持进程/用户匹配。当前模板没有这些字段，因此无需额外处理。

iOS 特有可用字段包括 `wifi_ssid` 和 `wifi_bssid`，但不是通用模板必需项，不建议默认加入。

## 内存

SFI 运行在 NetworkExtension 中，iOS 会对扩展施加系统内存压力。当前模板含约 26 个远程规则集，功能较重；语法可以通过不代表所有 iPhone/iPad 都不会被系统 Jetsam。

如果实机发生 OOM/服务被杀：

1. 优先删不用的平台规则集；
2. 减少超大广告规则；
3. 降低并发连接；
4. 在 SFI 的 OOM Report / Service Log 查看具体报告；
5. 不要额外启用 Clash API/WebUI。

## 校验

本地生成的 chain/standard × 三种 IP 偏好共六份草稿，均经 sing-box 1.14.0-alpha.48 `check` 通过。正式模板仍保留空 selector，等待 Sub-Store 填入节点。

GitHub `ios` 分支目前保持空分支，尚未上传这些草稿。
