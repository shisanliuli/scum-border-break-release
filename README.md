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

## SCUM 启动器 v0.4.0 · UE4SS DLL 安装测试版

[下载启动器社区发行包（Windows x64）](https://github.com/shisanliuli/scum-border-break-release/releases/tag/launcher-v0.4.0-test.1)

**启动器仍处于公开测试阶段，很多功能尚未完善或开放，建议目前仅用于启动已经安装 MOD 的游戏。**

- **UE4SS DLL 拖入安装**：支持 Windows x64 UE4SS C++ 模组；命名 DLL 自动安装为 `Mods/模组名/dlls/main.dll`。单独 `main.dll` 可从目录识别名称或弹窗输入。带资源/依赖的模组建议保留完整目录结构，以 ZIP/7Z/RAR 导入。
- **已有 UE4SS 检测与离线包**：支持 Win64 根目录和 `ue4ss` 子目录；缺少时提示导入与游戏兼容的完整离线包，不自动联网下载 UE4SS，不附送加载器或示例模组。
- **PAK 和 DLL 本地管理**：支持校验、启用、禁用、更新、上一版回滚和卸载。手动同名文件需确认后备份接管；DLL、PAK、离线环境同批提交并支持中断恢复。
- **五种语言**：简体中文、繁体中文、English、日本語、한국어，在设置页即时切换并保存。

请完整解压后运行 `SCUMDevLauncher.exe`，在“设置”选择并保存游戏根目录。导入前关闭游戏。发行包自带 .NET 10 Windows x64 运行环境，不含个人账号、私人配置或模组本体。

**在线模组下载与分发尚未开放。** 本版拖入安装使用玩家已有的本地文件；不支持自定义 UE4SS 路径、独立 Lua 模组、加密/分卷/嵌套压缩包、文件夹、网页链接、UTOC/UCAS 或自动执行安装脚本。DLL 导出/导入检查不保证真实游戏、UE4SS ABI 或所有模组依赖兼容；请使用可信作者与匹配版本。

核心回归 95 项、DLL 五语界面 28 项、原有多语言界面 67 项、实际发行 EXE 五语检查 30 项和全新启动 8 项通过。测试使用隔离假游戏；真实游戏内加载与服务器兼容性仍需进一步测试。请使用 0.4.0 管理本版 DLL 安装记录。

[更新说明与 SHA256](https://github.com/shisanliuli/scum-border-break-release/releases/tag/launcher-v0.4.0-test.1) · [上一测试版 v0.3.0](https://github.com/shisanliuli/scum-border-break-release/releases/tag/launcher-v0.3.0-test.1)

---

## 使用条款

- 本 mod 修改的是游戏原始资产，其版权归 **Gamepires / Epic Games** 所有。
- 请在你**拥有正版 SCUM** 的前提下使用。
- 允许个人使用与免费转载（转载请注明出处与本仓库地址）；
  **禁止** 用于商业售卖、二次打包收费、或拆分素材单独分发。
- 使用本 mod 造成的任何后果（存档异常、联机被封等）由使用者自行承担。

## 仓库内容

这里提供成品包、说明和兼容性清单；内部源码、构建密钥、个人存档和原始运行日志不在公开下载中。
