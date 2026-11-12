# SCUM 破边境（Border Break）

**v1.1.0：适配 SCUM 1.3.6 / CL 177121 / Steam BuildID 26593778。**

[下载 1.3.6 适配包](https://github.com/shisanliuli/scum-border-break-release/releases/tag/v1.1.0-scum1.3.6) · [验证状态](VALIDATION.md) · [更新记录](CHANGELOG.md)

本版重新构建边境拆墙地图，修复游戏更新后进存档时的 `WorldComposition / Serial size mismatch` 崩溃。已实测进入原存档、墙体消失并可通过；越界长时间停留和界外重新登录仍待验证，因此标记为预发布。

纯数据 PAK，适用于单人/自建存档，不需要本 MOD 的 UE4SS 原生模块，也不编辑存档。

## 从旧版升级

1. 正常退出游戏，备份存档和旧 MOD 文件。
2. 用本版 `pakchunk962-NoWall_P.pak` 替换旧 962；将 **`pakchunk963-NoWallFix_P.pak` 移出加载目录**。其他覆盖 `The_Island` 主地图的 MOD 也不能直接叠加。
3. 将下载包 `pak/` 中两个文件安装到：

   ```text
   .../SCUM/SCUM/Content/Paks/~Mods/
   ```

4. 使用已有兼容的 MOD 管理和正常启动流程进入存档，先确认加载和墙体通行。

966 计时包的原版源数据本次没有变化，重建后与旧包字节相同；可以按本版校验值核对已有文件。

旧 1.0.0 地图包与 1.3.6 不兼容。卸载本版时退出游戏，移出 962/966 即恢复原版资源；**不要将旧版地图包放回 1.3.6**。

## 功能及已验证范围

| 项目 | 本版状态 |
|---|---|
| 20 组边境墙网格和实例数清零 | 结构检查通过；用户实测位置的墙消失且可通过 |
| 进入原有单人存档 | 已通过，新日志无原序列化崩溃 |
| 出界检查间隔 | 数据为 1,000,000 秒，约 11.57 天；本版越界长留和重新登录仍待实测 |
| 出界伤害、KillZ 参数 | 保留既有数据调整；不等同于所有死亡途径均关闭 |
| 新增地图外地形 | 没有提供 |

本次验证没有逐一标明北/东两侧和全部墙段，也不代表服务器联机验证。1,000,000 秒是有限检查间隔，不承诺永久或无限生存。

## 游戏再次更新时

核对游戏构建号及 [COMPATIBILITY.json](COMPATIBILITY.json) 中的资源指纹；版本不匹配时需重新适配。清单本身不会阻止 Steam 更新或自动停用旧 MOD。

遇到加载崩溃，先退出游戏并停用旧版/冲突主地图包，保留存档和崩溃日志。不要通过改包编号来尝试修复资源格式不兼容。

## 文件与校验

| 文件 | 大小 | SHA256 |
|---|---|---|
| `pakchunk962-NoWall_P.pak` | 10,096,939 B | `81e1d3bd3edb50fda1ddb43864dbc438df52ff14473dd182ff4a18afd2783114` |
| `pakchunk966-OOBInterval_P.pak` | 111,373 B | `08cd7183913fb5b0ee37153dc38a14b86f02766558db4daf94df33acb92ef58b` |

```powershell
Get-FileHash .\pak\pakchunk962-NoWall_P.pak -Algorithm SHA256
```

完整文件校验见 [SHA256SUMS.txt](SHA256SUMS.txt)，下载 ZIP 的校验文件在同一发布页。

## 已知限制

- 尚未验证越界长留及界外退出重进；这是 1.1.0 预发布保留项。
- 地图外没有本 MOD 新增的可玩地形。
- 单人存档测试结果不能推广到全部服务器；联机使用应遵守服务器规则。
- 游戏或相关资源更新后，本版可能需要重建。

---

## SCUM 界跃（SCUM Rift）v0.5.0 · 社区测试版

<img src="docs/launcher/assets/rift-icon.png" alt="SCUM Rift 图标" width="72" />

[下载 Windows x64 社区发行包](https://github.com/shisanliuli/scum-border-break-release/releases/download/launcher-v0.5.0-test.1/SCUMRift-0.5.0-win-x64-test.zip) · [发布说明与校验](https://github.com/shisanliuli/scum-border-break-release/releases/tag/launcher-v0.5.0-test.1) · [使用说明](docs/launcher/使用说明.md)

**启动器仍处于公开测试阶段，很多功能尚未完善或开放，建议目前主要用于启动已经安装 MOD 的游戏。**

- **MOD / 纯净模式一键切换**：把标准位置的 PAK、LogicMods 和 UE4SS 环境移至游戏根目录的 `.SCUMRift-cache`，无需卸载或重新下载。恢复时保留配置与原启用状态；恢复目标出现新文件时会停止，保留两边内容。
- **Steam 启动顺序优化**：检查有效客户端、登录和会话稳定后再启动游戏，等待与模组校验同时进行；等待可取消，超时会停止本次启动。
- **新名称与图标**：SCUM 界跃 / SCUM Rift；桌面图标为紫灰底，窗口左上角直接绘制无背景矢量标志，随主题显示。
- **保留拖入与本地管理**：支持 PAK、UE4SS C++ DLL、ZIP、7Z、RAR；缺少 UE4SS 时支持导入自备兼容离线包。已管理模组可校验、启停、更新、回滚及卸载。
- **五种语言**：简体中文、繁体中文、English、日本語、한국어，在设置中切换并保存。

完整解压后运行 `SCUMDevLauncher.exe`，在“设置”中选择并保存游戏根目录。游戏关闭后再安装或切换模式；发行包自带 .NET 10 Windows x64 运行环境，不含个人账号、私人配置和模组本体。

**纯净切换覆盖文档列出的标准模组位置，不能还原被其他工具替换的官方游戏资源。** 请保留缓存区及管理记录，不要手动删除。**降级到 0.4.0 或更早版本、搬动游戏目录前，先使用 0.5.0 恢复 MOD 模式。**

**在线模组下载与分发尚未开放。** 拖入安装使用玩家已有的本地文件，UE4SS 不自动联网下载。自定义加载路径及未支持的模组布局需自行处理；真实 Steam 冷启动、游戏加载、服务器及更多系统环境的兼容性仍需实际游玩验证。

[更新记录](docs/launcher/更新记录.md) · [验收范围](docs/launcher/VALIDATION.md) · [上一测试版 v0.4.0](https://github.com/shisanliuli/scum-border-break-release/releases/tag/launcher-v0.4.0-test.1)

---

## 使用条款

- 本 mod 修改的是游戏原始资产，其版权归 **Gamepires / Epic Games** 所有。
- 请在你**拥有正版 SCUM** 的前提下使用。
- 允许个人使用与免费转载（转载请注明出处与本仓库地址）；
  **禁止** 用于商业售卖、二次打包收费、或拆分素材单独分发。
- 使用本 mod 造成的任何后果（存档异常、联机被封等）由使用者自行承担。

## 仓库内容

这里提供成品包、说明和兼容性清单；内部源码、构建密钥、个人存档和原始运行日志不在公开下载中。
