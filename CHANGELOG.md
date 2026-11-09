# 更新记录

## 启动器 v0.2.0 · 首个公开测试版（2026-11-09）

- 新增 [SCUM 启动器社区发行包](https://github.com/shisanliuli/scum-border-break-release/releases/tag/launcher-v0.2.0-test.1)，供 Windows x64 玩家测试。
- 这是启动器的第一个测试版，很多功能尚未完善或开放，**建议目前仅用于启动已经安装 MOD 的游戏**。
- 模组下载与在线分发暂未开放，其他模组管理功能仍处于测试阶段。
- 完整解压后运行 `SCUMDevLauncher.exe`，在设置中选择 SCUM 游戏目录并保存。

## v1.0.0

首个公开版本。

**包含**
- pakchunk962-NoWall_P.pak —— 移除岛屿边界（北端、东端）的全部石墙；放宽坠落下限。
- pakchunk966-OOBInterval_P.pak —— 关闭出界判死与出界伤害，越过地图边界后可以一直待在外面。

**安装**
1. 两个 pak 复制到 SCUM\Content\Paks\~Mods\
2. 启动参数加 `-fileopenlog`

**已知限制**
- 地图边界之外目前没有地形（只有海面与虚空）。
- 仅单机 / 自建存档有效；官方联机服务器不认这组 pak。
- 游戏更新后可能需要重新制作。

**验证状态**
- 资产结构校验：通过
- 游戏内行为验证：进行中