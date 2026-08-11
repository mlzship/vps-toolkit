# vps-toolkit

VPS 体检 + TCP 调优一体化工具：检测 → 诊断 → 调优 → 复测的闭环编排器。

只编排活跃上游、不 fork 代码：运行时现拉官方版本，永远用最新上游。

## 快速开始

```bash
# 交互菜单（推荐）
bash <(curl -fsSL https://raw.githubusercontent.com/mlzship/vps-toolkit/main/vps-toolkit)

# 或安装后使用
curl -fsSL https://raw.githubusercontent.com/mlzship/vps-toolkit/main/vps-toolkit -o /usr/local/bin/vps-toolkit
chmod +x /usr/local/bin/vps-toolkit
ln -sf /usr/local/bin/vps-toolkit /usr/local/bin/vt
vps-toolkit
```

## 功能

### 检测（编排上游）

| 上游 | 用途 |
|---|---|
| [xykt/IPQuality](https://github.com/xykt/IPQuality) | IP 质量/风险深度体检 |
| [oneclickvirt/ecs](https://github.com/oneclickvirt/ecs)（融合怪） | 系统/CPU/内存/磁盘/流媒体/回程/测速综合体检 |
| [ibsgss/TcpQuality](https://github.com/ibsgss/TcpQuality) | TCP 重传 + 全国 93 节点回国探测 |

### TCP 调优

- 内置精简 BBR 调优：BBR + fq + 按内存推导的缓冲区（快照可回滚）
- 编排 [Kylin010/tcpfit](https://github.com/Kylin010/tcpfit)：实测推导的智能调优、限速器扫描（sweep）、整形（shape）
- 冲突防护：检测既有调优配置，禁止静默叠加
- 一键回滚到调优前

### 闭环 boost

基线测试 → 应用调优 → 复测 → 前后对比报告，一条命令验证调优收益。

## 命令行（全部功能支持非交互）

```
vps-toolkit quick|full            # 快速/完整体检
vps-toolkit ip|ecs|tcp            # 单项检测
vps-toolkit tune --bbr|--tcpfit   # 调优
vps-toolkit tune --rollback       # 回滚
vps-toolkit boost [--bbr|--tcpfit]# 闭环
vps-toolkit reports|update|status
```

报告保存在 `/root/vps-toolkit-reports/<时间戳>/`（各上游完整日志 + SUMMARY.md）。

## 设计原则

- **零遥测**：除 ipinfo.io 画像与官方源下载外无任何外联
- **下载必校验**：shebang / SHA256，绝不绕过证书校验
- **改动必快照**：调优前保存全部原值，rollback 逐项还原
- **CJK 真对齐**：按 UTF-8 字节计算显示宽度，菜单不错位

## 路线图

- v0.2：XanMod BBRv3 内核（Debian/Ubuntu x86_64）、场景化内核参数（web/stream/game）、集群批量执行、英文界面

## English Summary

vps-toolkit is an orchestrator (single-file bash) for VPS benchmarking and TCP tuning: it runs best-in-class upstream tools (IPQuality, ecs, TCPQuality, tcpfit) with a unified interactive menu, snapshot-based rollback, and a baseline→tune→retest closed loop. No telemetry; downloads are always verified.

## License

MIT
