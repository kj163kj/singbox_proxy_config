# 📦 Sing-Box_proxy_config

一个用于存放 [sing-box](https://sing-box.sagernet.org/) 当前配置模板的仓库。

> [!IMPORTANT]
> 当前配置仅支持 sing-box `v1.14.0-alpha+`。旧版配置已删除，请先升级客户端或核心。
>
> 本仓库只维护当前配置，不提供旧版本 Tag 或 Release；更新会直接覆盖原文件。

## 🖥️ 平台分支

| 分支 | 适用平台 |
|---|---|
| [`sfa-sfw`](../../tree/sfa-sfw) | sing-box for Android（SFA）与 sing-box for Windows（SFW） |
| [`sfi`](../../tree/sfi) | sing-box for iOS（SFI）TestFlight 测试版，仅支持 `v1.14.0-alpha+` |
| [`sfm`](../../tree/sfm) | sing-box for macOS（SFM），未经实机测试，有问题请通过 Issues 反馈 |
| [`box-for-root`](../../tree/box-for-root) | Android Root 环境的 [Box for Root](https://github.com/boxproxy/box) |
| [`openwrt-momo`](../../tree/openwrt-momo) | OpenWrt 的 [OpenWrt-momo](https://github.com/nikkinikki-org/OpenWrt-momo) |

每个平台分支均包含：

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
> 这些是配置模板，部分 selector 的 `outbounds` 需由 Sub-Store 填入真实节点。未渲染时出现 `missing tags` 属于模板占位，不是字段错误。

## 🚀 使用说明

建议搭配 [Sub-Store 脚本](https://github.com/xream/scripts) 使用，实现订阅转换、节点筛选及策略组填充。

- [使用 Sub-Store 动态生成 sing-box 配置](https://www.tsy.ink/archives/2025/08/?p=101)
- [使用 Sub-Store 动态生成 sing-box 链式代理配置](https://www.tsy.ink/archives/2025/08/?p=118)

## 🔐 Clash API 安全提醒

配置中的以下内容是公开模板值，使用前必须检查：

```json
{
  "experimental": {
    "clash_api": {
      "external_controller": "127.0.0.1:20123",
      "secret": "CHANGE_ME_BEFORE_USE"
    }
  }
}
```

1. 把 Clash API 端口改为未被占用的端口；
2. 将 `secret` 改为你自己生成的随机密钥；
3. 不要把真实密钥提交到公开仓库；
4. `127.0.0.1` 只允许本机访问；改成 `0.0.0.0` 或局域网地址会扩大暴露范围；
5. 远程访问时必须设置强密钥并通过防火墙限制来源；
6. OpenWrt-momo 用户应优先在 Momo 的“外部控制”设置里配置 API 端口和密钥。

> [!WARNING]
> 如果真实密钥曾被公开，请立即更换。删除当前文件无法清除提交历史、Fork 或缓存中的密钥。

## ✅ 配置检查

订阅转换完成后建议检查最终配置：

```bash
sing-box check -c config.json
```

不要为了让未渲染模板通过检查，而把本应代理的空节点组永久改成直连。

## 🛠️ 开源许可

本项目遵循 MIT License 开源协议。

## 🙏 感谢

- [sing-box 官方项目](https://github.com/SagerNet/sing-box)
- [Sub-Store 脚本作者 xream](https://github.com/xream/scripts)
- [Box for Root](https://github.com/boxproxy/box)
- [OpenWrt-momo](https://github.com/nikkinikki-org/OpenWrt-momo)
- [GUI.for.Cores Plugin Hub](https://github.com/GUI-for-Cores/Plugin-Hub)
