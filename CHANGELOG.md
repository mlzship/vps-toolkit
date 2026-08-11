# Changelog

## v0.1.1 (2026-08-12)

- 修复流量计量 awk 函数定义位置错误（mawk/gawk 均报语法错误）
- 修复 IPQuality 误判：其脚本出报告后也可能退出非 0，改以报告链接判定成功
- 修复报告链接提取误捕获用法示例行

## v0.1.0 (2026-08-12)

首个公开发布版：

- 交互菜单（中文、CJK 对齐、流量计量、确认框、文件锁）
- 检测编排：IPQuality / ecs（goecs）/ TCPQuality，汇总 SUMMARY.md
- TCP 调优：内置精简 BBR 调优（按内存推导缓冲区）+ tcpfit 编排 + 冲突防护 + 完整回滚
- boost 闭环：基线 → 调优 → 复测 → 对比报告
- 自更新：release tag + SHA256SUMS 校验 + .bak 回滚
- `vt` 快捷别名，全部功能支持 CLI 非交互
