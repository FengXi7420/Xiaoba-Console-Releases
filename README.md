<div align="center">
  <img height="128" src="docs/branding/m-control-repository-icon.png" alt="小吧控制台 Logo">

  # 小吧控制台

  [![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D4?logo=windows&logoColor=white)](#下载和安装)
  [![.NET Framework](https://img.shields.io/badge/.NET%20Framework-4.6.2-512BD4?logo=dotnet&logoColor=white)](#下载和安装)
  [![Downloads](https://img.shields.io/github/downloads/FengXi7420/Xiaoba-Console-Releases/total?color=brightgreen)](https://github.com/FengXi7420/Xiaoba-Console-Releases/releases)
  [![MSI laptops](https://img.shields.io/badge/MSI-laptops-D23D1D)](#兼容性)
  [![Telemetry](https://img.shields.io/badge/telemetry-none-success)](#隐私和网络访问)
</div>

## 🚨 Project Status Notice

> [!IMPORTANT]
> - 小吧控制台仍处于主动开发阶段，硬件控制能力会优先根据真实 MSI 笔记本反馈迭代。
> - 当前发布包、问题反馈与文档入口为 [FengXi7420/Xiaoba-Console-Releases](https://github.com/FengXi7420/Xiaoba-Console-Releases)。
> - 本项目不隶属于 MSI / Micro-Star International，也不是 MSI 官方软件。
> - 本项目会直接访问 EC、MSI WMI、UEFI、NVAPI / NVML、SteelSeries HID 等硬件接口，请在使用前阅读免责声明和风险说明。

#### Other language versions of this README file:

- 简体中文：当前文件
- English: [README_EN.md](README_EN.md)

---

小吧控制台是一个面向 MSI 笔记本的轻量级 Windows 硬件控制工具。它的目标是替代 MSI Center / Dragon Center 中常用但分散的硬件控制能力，包括实时监控、风扇曲线、性能模式、显卡模式、电池健康、SteelSeries 键盘灯效、快捷键 OSD、驱动支持页入口和版本检查。

项目设计方向接近 [G-Helper](https://github.com/seerge/g-helper) 与 [Lenovo Legion Toolkit](https://github.com/LenovoLegionToolkit-Team/LenovoLegionToolkit)：保留笔记本控制中心里真正需要的功能，减少后台服务、弹窗、账号体系和无关模块。小吧控制台不做遥测，不收集用户数据；需要常驻时进入托盘，不需要时可以完全退出。

## 📖 快速开始

- [快速开始指南](docs/QUICKSTART.md) - 5 分钟上手教程
- [常见问题 FAQ](docs/FAQ.md) - 解决常见问题
- [兼容性列表](docs/COMPATIBILITY.md) - 查看你的机型是否支持

# Localization / 本地化

当前主界面和中文 README 已覆盖主要功能说明；英文 README 已加入项目概览、安装要求、功能说明、风险提示和构建方式。后续如果有更多机型适配数据，会继续补充英文兼容性说明和故障排查文档。

欢迎提交翻译和机型适配信息。由于 MSI 不同机型的 EC、WMI、灯光、GPU 模式和驱动栈差异较大，翻译内容应尽量与实际功能状态保持一致。

## 项目图标

项目图标资源放在 `docs/branding/`：

- `m-control-repository-icon.png`：512×512 方形图标，适合用作 GitHub 用户 / 组织头像，或支持“仓库头像”的代码托管平台。
- `m-control-social-preview.png`：1280×640 社交预览图，适合上传到 GitHub 仓库的 Social preview。

注意：GitHub 仓库标题左侧的小图标来自仓库所有者头像，不是仓库内某个文件。如果需要标题栏像截图中的 LenovoLegionToolkit 一样显示项目图标，需要在 GitHub 用户 / 组织头像处上传 `m-control-repository-icon.png`。仓库分享卡片则使用 `m-control-social-preview.png`。

---

# Table of Contents / 目录

- [快速开始](#快速开始)
- [Localization / 本地化](#localization--本地化)
- [项目图标](#项目图标)
- [免责声明](#免责声明)
- [闭源免费说明](#闭源免费说明)
- [下载和安装](#下载和安装)
- [兼容性](#兼容性)
- [主要功能](#主要功能)
- [设计目标](#设计目标)
- [风扇校准](#风扇校准)
- [命令行参数](#命令行参数)
- [诊断日志](#诊断日志)
- [构建](#构建)
- [测试](#测试)
- [发布打包](#发布打包)
- [项目结构](#项目结构)
- [隐私和网络访问](#隐私和网络访问)
- [反馈与适配](#反馈与适配)
- [风险说明](#风险说明)
- [License](#license)

---

## 免责声明

**小吧控制台不是 MSI 官方软件，不提供任何官方保修或官方支持。**

本项目会访问和修改 EC、MSI WMI、UEFI 变量、WinRing0、SteelSeries HID 等硬件接口，并通过 NVAPI / NVML 读取显卡遥测。不同 MSI 机型、BIOS、EC 固件和驱动版本的行为可能不同。风扇曲线、GPU 模式、功耗限制、键盘灯效和快捷键功能都应以真实设备验证为准。

使用本项目造成的硬件异常、系统不稳定、数据丢失、保修争议或其他后果，均由使用者自行承担。

---

## 闭源免费说明

小吧控制台当前以闭源免费方式发布。软件需要与 MSI 笔记本的 EC、风扇控制器、键盘灯效、GPU 模式等底层硬件接口通信，部分兼容性实现涉及未公开接口、私有协议适配和逆向分析资料。为了避免公开实现细节后引发不必要的知识产权或合规风险，也为了让项目能够长期维护和更新，当前版本不公开项目代码。

小吧控制台不做遥测，不收集用户数据，不读取个人文件。核心硬件控制功能主要在本机执行；发布包会提供 SHA256 校验值，用户可以自行校验，也可以用杀毒软件或虚拟机环境进行验证。如果你无法接受闭源工具，可以选择不使用或先观望后续发布记录。

---

## 下载和安装

### 快速下载

从 [GitHub Releases](https://github.com/FengXi7420/Xiaoba-Console-Releases/releases) 下载最新版本：

- **安装包（推荐）**：`MControl_v<版本号>_Setup.exe` - 自动安装依赖项
- **便携版**：`MControl_v<版本号>_Portable.zip` - 免安装；便携版不会自动安装 PawnIO，依赖 CPU MSR/EC 的功能需手动安装驱动
- **WebView2 Fixed 安装版**：`MControl_v<版本号>_Setup_WebView2_Fixed.exe` - 真正内嵌固定版 x64 Runtime；基线版本和 hotfix 都可以提供该安装包

小吧控制台 v1.0.0 是本发行线的覆盖升级基线。M-Control v1.1.0 及更高版本可直接安装小吧控制台替换，更早的 M-Control 建议先卸载；后续小吧控制台版本可从 v1.0.0 直接覆盖升级。安装器会复用原安装目录、关闭旧版前台与后台进程，并只清理小吧控制台自己登记的废弃文件；不承诺清理所有更早历史版本残留。

**首次使用？** 查看 [快速开始指南](docs/QUICKSTART.md) 了解详细安装步骤。

### 运行要求：

- Windows 10 / 11 x64。
- .NET Framework 4.6.2。
- Microsoft Edge WebView2 Runtime。
- MSI ACPI WMI Provider / MSIWMIACPI2 相关平台驱动。
- WinRing0 运行时文件，用于 EC / MSR 兜底访问。
- NVIDIA 驱动、NVAPI / NVML / nvidia-smi，用于 NVIDIA GPU 只读监控。
- SteelSeries 键盘灯效优先使用已枚举到的 HID 设备；若用户本机已安装 GG / SteelSeries 并开出高级 KLC 通道，小吧控制台会自动使用，否则优先走免驱 HID 路径。发布包不内置 `ssdevfactory` / `ssps2` / `msihid`。
- 部分底层硬件访问需要管理员权限。

---

## 兼容性

小吧控制台面向 MSI 笔记本，尤其是支持 EC 风扇控制、MSI WMI、独显模式切换和 SteelSeries 键盘灯效的机型。

**📋 查看详细兼容性信息：[兼容性列表](docs/COMPATIBILITY.md)**

兼容性取决于以下因素：

- 机型和主板平台。
- BIOS 和 EC 固件版本。
- MSI ACPI WMI Provider / MSIWMIACPI2 驱动状态。
- NVIDIA 驱动、NVAPI / NVML 支持情况。
- SteelSeries 键盘 PID、HID 通道和驱动栈。
- ThermalInfo、IPF / DTT、LibreHardwareMonitor、MSR 等传感器链路可用性。

已知限制：

- 没有对应 EC 寄存器或 WMI 命令的功能不会显示或不会启用。
- 没有独显或不支持 MUX 的机型不会提供完整显卡模式切换。
- SteelSeries 灯效功能需要匹配键盘设备、驱动和协议。
- 第三 / 第四风扇、PCH、系统功耗等扩展传感器按实测能力显示，不强行伪造数据。

---

## 主要功能

### 仪表盘

- CPU / GPU 温度、频率、功耗、电池状态和风扇状态。
- AMD 平台 CPU 温度优先使用 Feature Manager 同源的 ThermalInfo `Get_Temperature(0)` CPU，失败后回退 ThermalInfo AMD SENSOR `Get_BIOS(3)`、通用 ThermalInfo 和 EC；CPU 功耗优先使用 PawnIO/MSR RAPL AMD package，失败后回退 LHM / WMI / ThermalInfo。
- 风扇 RPM 和百分比显示切换；百分比模式需要风扇校准。
- 风扇 RPM 优先读取 ThermalInfo `Get_Fan(0)`，EC 直读作为兜底。
- 扩展传感器支持 PCH、第三 / 第四风扇和系统功耗等机型相关项目。
- 监控数据采用快慢路径分离，优先展示核心健康数值，较慢的扩展传感器在后台补齐。

### 风扇控制

- CPU / GPU 风扇曲线独立编辑。
- 支持自动 / 手动模式、曲线拖拽和表格数值编辑。
- 纵坐标使用 RPM；EC duty 按 0-150 处理，最高显示 9000 RPM（150 × 60）。
- 恢复启动曲线会回到小吧控制台本次启动、首次写入风扇前捕获的硬件曲线快照。
- 风扇曲线读写优先使用 ThermalInfo 官方 `Get_* / Set_*`，失败后使用 EC 兜底。
- 百分比显示校准使用 IQR 离群剔除和中位数基准，减少异常 RPM 读数带来的误差。
- 支持全转速模式，固定快捷键 `Fn + ↑` 也可切换。

### 性能、电源和显卡模式

- 平衡、安静、节能、高性能四档性能模式。
- 启动时同步当前真实性能模式。
- Windows 电源计划可与性能模式配合管理。
- GPU 模式支持核显、混合和独显。
- GPU 模式切换后可选择立即重启或稍后重启。

### GPU 监控

- 只读显示 NVIDIA GPU 温度、频率、功耗、利用率和风扇状态。
- 主分支不提供 GPU 超频、锁频、VF 曲线或游戏帧数检测功能；相关实验实现仅保存在独立开发分支。

### 电池

- 电池充电上限设置。
- 健康度、循环次数、设计容量、满充容量、当前容量、电压等信息。
- 电池电流读数包含方向和单位修正，避免充放电状态显示错误。

### SteelSeries 键盘灯效

- 区域分组、效果切换、调色板、亮度和速度。
- 支持 SteelSeries 原生 KLC HID 和 SteelSeries 免驱基础 HID；若系统已有 GG / SteelSeries 开出的高级 KLC 通道会自动使用，但小吧控制台不提供 SteelSeries 驱动安装。
- 不要求安装 SteelSeries GG；动态效果使用已内置的实机 HID 采样和原生写入逻辑。
- 发布包不附带 `ssdevfactory` / `ssps2` / `msihid` 驱动资源，也不默认混入未验证的 SteelSeries 驱动组件。
- 支持逐键编辑、官方键位映射、局部区域写入、动态效果、响应层和灯效宿主接管。
- Raider 18 / KLC071 / PID_1122 / PID_1161 等新老 SteelSeries 设备包含独立适配逻辑。

### 快捷键和 OSD

- 固定快捷键：`Fn + ↑` 切换风扇全转速，`Fn + F4` 切换触摸板。
- 信息页“快捷键说明”中的实际快捷键会尽量接入左上角 OSD。
- OSD 只显示状态提示，不接管系统原功能。
- 能读取真实状态的功能显示开启 / 关闭；无法可靠读取状态的功能显示已触发 / 已切换。
- 覆盖范围包含 CapsLock、触摸板、风扇全速、Win/Fn 交换、音量、亮度、截图、显示输出、键盘背光、媒体、睡眠、麦克风、蓝牙、Fn Lock、准星、Scroll Lock 等。
- 快捷键事件来源包括低级键盘 Hook、MSI WMI 热键事件和 EC debug register，并包含去重逻辑。

### 驱动、信息和应用行为

- 驱动更新页跳转到 MSI 中国官网对应机型 BIOS / 驱动支持页。
- 驱动更新页仅提供当前机型的 MSI 官网支持页、BIOS、驱动程序和说明书四个入口，不在软件内扫描、下载或安装驱动。
- 硬件信息页显示机器、CPU、GPU、内存、磁盘和快捷键说明。
- 关于页提供版本检查、忽略版本和自动检查入口。
- 支持启动行为、关闭到托盘、开机自启、启动最小化和退出时保留灯效。
- 主程序包含单实例守卫，重复启动会唤醒已有窗口。

---

## 设计目标

小吧控制台不尝试复刻 MSI Center 的全部模块，而是聚焦笔记本日常控制场景：

- 常用控制集中在一个轻量工具里。
- 减少常驻服务、弹窗、账号系统和无关在线模块。
- 尽量直接使用硬件接口和本地驱动，不建立额外后台链路。
- 功能不可用时明确降级或隐藏，不展示误导性的假状态。
- 不做遥测，不收集用户数据。

---

## 风扇校准

风扇校准用于仪表盘风扇百分比模式。由于不同 MSI 机型的 PWM / duty 读数并不稳定，小吧控制台使用实际 RPM 样本估算满速基准。

校准流程：

1. 开启全转速并等待风扇加速。
2. 以 1Hz 采样收集 RPM。
3. 过滤 0 和明显不合理的物理值。
4. 使用 IQR 剔除离群样本。
5. 使用中位数作为满速基准。
6. 运行时使用 `current_rpm / RpmRef × 100` 计算百分比，并加入上限防抖。

校准结果保存到 `%LocalAppData%\M-Control\fan-calibration.json`，并按机型区分。

---

## 命令行参数

常用启动参数：

- `--background`：后台启动，不主动显示主窗口。
- `--minimized`：最小化启动。

如果已有实例正在运行，普通重复启动会唤醒已有窗口；后台启动参数不会强制弹出已有窗口。

---

## 诊断日志

小吧控制台提供两级日志系统：

### 1. 错误日志（默认开启）

所有硬件操作失败、配置加载错误等异常都会自动记录到：
- `%LocalAppData%\M-Control\error.log`

日志格式：
```
[2026-06-20 02:15:30] WARN Failed to read GPU temperature via NVAPI
System.Exception: NVAPI error code 5
   at MControl.Core.GpuTelemetryController.CollectTelemetryUncached()
   ...
```

### 2. 诊断日志（手动开启）

需要详细排查时，在 `%LocalAppData%\M-Control\debug.flag` 创建空文件并重启应用。

常见诊断日志：
- `telemetry_debug.txt`：CPU / GPU 频率、功耗和传感器读数。
- `fan_debug.txt`：风扇 RPM、百分比和解析路径。
- `monitor_push_debug.txt`：前端监控 payload。
- `gpu_mode_read_debug.txt`：GPU 模式探测路径。
- `errors.txt`：后端错误（debug 模式专用）。
- `errors_js.txt`：前端 JavaScript 错误。
- `hotkey_debug.txt`：快捷键和 EC debug register 事件。

删除 `debug.flag` 后重启即可关闭诊断日志。

---

## 构建

以下命令默认从仓库根目录执行：

```powershell
dotnet build .\MControl.sln -c Release
```

输出路径：

```text
01_source\MControl\bin\Release\net462\MControl.exe
```

构建要求：

- Windows 10 / 11 x64。
- .NET SDK，可构建 .NET Framework 4.6.2 项目。
- Microsoft Edge WebView2 Runtime。
- 管理员权限用于运行时硬件访问。

`Mono.Posix` 相关 warning 来自依赖链，在当前 net462 Windows 运行路径中不会影响构建结果。

---

## 测试

前端 JavaScript 语法检查：

```powershell
Get-ChildItem .\01_source\MControl\Web -Filter app*.js | ForEach-Object { node --check $_.FullName }
```

运行全部静态冒烟测试：

```powershell
Get-ChildItem .\01_source\tests -Filter *.test.js | ForEach-Object { node $_.FullName }
```

这些测试主要用于锁定关键 UI、硬件路径和文档结构，避免后续改动误删已确认的功能入口。

---

## 发布打包

以下命令默认从仓库根目录执行：

```powershell
powershell -File .\02_build\scripts\Publish-MControl.ps1
```

脚本会执行：

1. 默认自动递增三段公开版本号的补丁位，并同步前端、Assembly、manifest 和 Inno 配置。
2. `dotnet publish` 输出到 `02_build\publish_final_yyyyMMdd_HHmmss\`。
3. 清理运行时 debug 文本和临时诊断文件。
4. 清理旧前端残留产物。
5. 生成 `02_build\MControl_v{版本号}_Portable.zip`。
6. 指定 `-IncludeWebView2OfflinePortable` 时，额外生成 `02_build\MControl_v{版本号}_Portable_WebView2_Offline.zip`。
7. 指定 `-IncludeWebView2FixedRuntimeInstaller` 时，额外生成真正内嵌固定版 Runtime 的 `03_exe\MControl_v{版本号}_Setup_WebView2_Fixed.exe`。
8. 检测到 Inno Setup 6 时生成 `03_exe\MControl_v{版本号}_Setup.exe`。
9. 生成 `02_build\SHA256SUMS.txt`，用于发布页校验。

可选参数：

- `-SkipInstaller`：跳过 Inno Setup 安装包生成。
- `-NoVersionBump`：不递增版本号，仅用当前源码版本重打包；适合本地调试或复现旧包。
- `-IncludeWebView2OfflinePortable`：额外生成附带微软官方 x64 WebView2 离线安装程序的便携 ZIP。
- `-WebView2OfflineInstallerPath <path>`：使用本机已有的微软官方 x64 离线安装程序；未指定时从微软官方入口下载到忽略的构建缓存。
- `-IncludeWebView2FixedRuntimeInstaller`：额外生成真正内嵌微软官方 x64 WebView2 Fixed Version Runtime 的安装包；基线版本和 hotfix 都支持。
- `-WebView2FixedRuntimeDirectory <path>`：使用本机已展开的固定版 Runtime；未指定时下载、验签并缓存脚本锁定的官方 CAB。
- `-InnoSetupExe <path>`：指定 `ISCC.exe` 路径。

---

## 项目结构

```text
01_source/MControl/        主程序源码
├── MControl.csproj        net462 / x64 / WinExe
├── Program.cs                程序入口、DPI、单实例相关启动流程
├── MainForm.cs               主窗口和硬件控制核心逻辑
├── MainForm.HostBridge.cs    WebView2 与 C# JSON RPC 路由
├── MainForm.Tray.cs          托盘、自启、窗口恢复
├── MainForm.Monitor.cs       仪表盘采样和扩展传感器
├── MainForm.DriverUpdate.cs  MSI 支持页和驱动备份
├── MainForm.Shortcut.cs      快捷键、MSI WMI 热键和键盘 Hook
├── MainForm.Osd.cs           OSD 触发和快捷键映射
├── MainForm.Touchpad.cs      触摸板状态读写
├── Core/                     EC、WMI、GPU、灯光和传感器硬件层
├── Services/                 日志与原子文件基础设施
│   ├── Logger.cs             文件日志系统（支持格式化）
│   └── AtomicFile.cs         同目录临时文件与原子替换
└── Web/                      WebView2 前端页面、样式和脚本

02_build/                     构建脚本和发布产物目录
03_exe/                       Inno Setup 安装包输出目录
01_source/tests/              Node 静态冒烟测试
```

---

## 隐私和网络访问

小吧控制台不做遥测，不收集用户数据，不上传硬件信息。

可能发生的网络访问：

- 用户打开驱动更新页时，跳转到 MSI 官网支持页面。
- 用户使用版本检查功能时，请求 GitHub 更新仓库 Release 信息。

除此之外，核心硬件控制功能均在本机执行。

---

## 反馈与适配

欢迎提交：

- 新机型的兼容性反馈。
- BIOS / EC 版本与功能可用性记录。
- 风扇、GPU 模式、触摸板、灯光、快捷键的实机测试结果。
- 文档、翻译、安装体验和官网内容建议。

提交问题时建议包含：

- 具体机型。
- Windows 版本。
- BIOS / EC 版本。
- MSI 相关驱动版本。
- NVIDIA 驱动版本。
- 问题复现步骤。
- 开启 `debug.flag` 后生成的相关日志。

---

## 风险说明

- EC 写入可能影响风扇、电池、键盘、GPU 模式和系统稳定性。
- 风扇曲线、全转速、功耗墙和 GPU 模式切换建议先在测试机上验证。
- 触摸板和快捷键在不同 MSI 机型上差异较大。
- SteelSeries 灯效会受到 PID、固件、驱动栈和 HID 通道影响。
- 某些 WMI 能力仍依赖 MSI ACPI WMI Provider。

---

## License

当前版本采用闭源免费授权。你可以在个人设备上免费安装和使用发布包，但不得商业售卖、二次打包冒充原作者、删除或篡改作者署名，也不得声明本项目与 MSI 存在官方授权或合作关系。
