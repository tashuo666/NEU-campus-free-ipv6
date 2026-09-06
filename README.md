# NEU-campus-free-ipv6

面向支持公网 IPv6 的 NAT 服务器的 Sing-box 部署脚本。

## 功能

- 仅生成公网 IPv6 节点
- VLESS Reality、Hysteria2、AnyTLS、Trojan、Shadowsocks 2022
- 每个协议独立端口
- 支持自定义端口或随机端口
- 使用公网 IPv4 提供订阅下载
- 提供两种 Clash 订阅：校园网免流和普通国内外分流

## 订阅地址

订阅服务使用公网 IPv4，节点连接使用公网 IPv6：

```text
http://公网IPv4:订阅端口/UUID/clash-campus-free
http://公网IPv4:订阅端口/UUID/clash
```

`clash-campus-free` 使用校园网网段直连、IPv6 分流和免流节点规则；`clash` 使用普通国内外分流规则。

## 安装

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/tashuo666/NEU-campus-free-ipv6/main/sing-box.sh)
```

脚本会检测公网 IPv6。内网 IPv6、ULA、链路本地地址和多播地址不会被用于节点。

## 端口模式

交互安装时选择：

- 自定义端口：分别输入 VLESS Reality、Hysteria2、AnyTLS、Trojan、Shadowsocks 端口。
- 随机端口：为五个协议分别生成未占用端口。

也可以使用参数：

```bash
bash sing-box.sh --PORT_MODE random --SUBSCRIBE_IP 82.156.239.160
```

NAT 服务商必须为五个 IPv6 节点端口提供入站放行；订阅端口则必须通过公网 IPv4 映射并放行。

## 前置条件

1. NAT 服务器拥有可公网访问的 Global IPv6。
2. 客户端网络支持 IPv6。
3. NAT 服务商允许 IPv6 TCP/UDP 入站。
4. 公网 IPv4 订阅端口已映射到 Nginx。
5. 防火墙和云安全组已放行订阅端口及节点端口。

## 重要说明

Clash 规则只能决定流量走直连还是代理，不能保证运营商一定按照免流计费。实际效果取决于校园网/运营商的 IPv4、IPv6 白名单和计费策略。

