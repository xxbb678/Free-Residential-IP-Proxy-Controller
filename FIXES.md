# 已修复问题

本 Fork 收录了实际部署中修复的节点 Agent 代码，位于 `agent/`。

## 修复内容

- 修复面板错误上报 Cloudflare/WARP 出口地址的问题，支持通过 `PUBLIC_IP` 指定真实 VPS 入口地址。
- 主隧道和备用隧道分别维护独立的故障计数，避免一条线路的状态干扰另一条线路。
- 检测 OpenVPN 进程退出、TUN 接口消失以及连续 HTTP/ICMP 探测失败。
- 故障后自动清理隧道对象状态，使节点池能够自动选择新节点并重建隧道。
- 连续三次探测失败后惩罚并拉黑故障入口 IP，避免立即重复选中。
- 主线路故障时优先切换到健康备用线路，后台自动补齐备用线路。
- Web 和代理凭据改为从环境变量读取，仓库不保存实际密码。

## Agent 环境变量

```bash
WEB_USER=admin
WEB_PASS=change-me
PROXY_USER=proxy
PROXY_PASS=change-me
PUBLIC_IP=你的VPS公网入口IP
```

不要把真实密码提交到 GitHub。
