# 常见问题 (FAQ)

## 安装和启动问题

### Q1: 安装后打不开怎么办？

**可能原因和解决方案：**

1. **缺少 .NET Framework 4.6.2**
   - Windows 10/11 通常已内置
   - 运行 Windows Update 更新系统
   - 手动下载：https://dotnet.microsoft.com/download/dotnet-framework/net462

2. **缺少 WebView2 Runtime**
   - 下载地址：https://developer.microsoft.com/microsoft-edge/webview2/
   - 选择 "Evergreen Standalone Installer" 下载并安装

3. **被安全软件拦截**
   - 检查杀毒软件是否拦截了程序
   - 将 MControl.exe 添加到白名单

### Q2: 提示权限不足怎么办？

**解决方案：**

1. **右键程序图标** → **以管理员身份运行**
2. 或在快捷方式属性中设置：
   - 右键快捷方式 → 属性
   - 点击"高级"按钮
   - 勾选"用管理员身份运行"
   - 确定并应用

**为什么需要管理员权限？**
- 访问 EC（嵌入式控制器）需要底层硬件权限
- 读写 WMI ACPI 接口需要系统权限
- 安装 PawnIO 驱动需要管理员权限

---

## 功能问题

### Q3: 某个功能显示灰色/不可用？

**常见原因：**

1. **没有管理员权限** → 以管理员身份运行
2. **机型不支持** → 查看[兼容性列表](COMPATIBILITY.md)
3. **驱动缺失** → 检查是否安装了 MSI Center 或相关驱动
4. **硬件不支持** → 例如没有 MUX 时无法切换完整 GPU 模式

### Q4: 和 MSI Center 会冲突吗？

**建议：**

- **不要同时运行** MSI Center 和小吧控制台
- 两个软件都会控制风扇、性能模式、GPU 模式
- 同时运行可能导致设置互相覆盖

**如何选择：**
- 如果只需要硬件控制，可以卸载 MSI Center，只用小吧控制台
- 如果需要 MSI Center 的其他功能（如 RGB 灯效联动），可以保留但不同时运行

### Q5: 风扇曲线怎么调才合理？

**建议原则：**

1. **不要过于激进**
   - 温度过低时风扇转速不宜太高（噪音大）
   - 温度上升时逐渐提高转速

2. **参考默认曲线**
   - 点击"恢复默认"查看 BIOS 默认设置
   - 在默认基础上微调

3. **测试验证**
   - 运行游戏或压力测试
   - 观察温度是否在安全范围（CPU < 95°C，GPU < 87°C）
   - 调整后再次测试

**示例曲线：**
```
温度 | CPU风扇 | GPU风扇
-----|---------|--------
50°C | 2000RPM | 2000RPM
60°C | 2500RPM | 2500RPM
70°C | 3500RPM | 3500RPM
80°C | 4500RPM | 4500RPM
90°C | 6000RPM | 6000RPM
```

## 卸载和清理

### Q6: 卸载后如何清理配置？

**配置文件位置：**
- `%LocalAppData%\M-Control\` （用户配置和日志）
- `%AppData%\M-Control\` （应用数据）

**清理步骤：**
1. 运行卸载程序
2. 手动删除上述文件夹
3. （可选）卸载 PawnIO 驱动：
   ```
   以管理员身份运行 PowerShell：
   PawnIO_setup.exe -uninstall
   ```

---

## 兼容性问题

### Q8: 哪些机型经过测试？

详见 [兼容性列表](COMPATIBILITY.md)

**已测试并支持：**
- Raider 系列
- Titan 系列
- Stealth 系列
- 部分 Cyborg 系列

**可能不支持：**
- 非 MSI 笔记本
- 台式机（部分功能可能可用）
- 特别老的机型（2020年前）

### Q9: 能否在没有 MSI 笔记本上运行？

**可以运行，但功能受限：**

- ✅ 可以启动程序
- ❌ 风扇控制不可用
- ❌ 性能模式切换不可用
- ❌ GPU 模式切换不可用
- ⚠️ GPU 监控可能可用（如果有 NVIDIA 显卡）
- ⚠️ 部分传感器可能可用

---

## 问题反馈

### Q10: 如何报告 Bug？

**反馈步骤：**

1. **生成诊断报告**
   - 打开软件
   - 点击"关于" → "生成诊断报告"
   - 保存 ZIP 文件

2. **提交 Issue**
   - 访问：https://github.com/FengXi7420/Xiaoba-Console-Releases/issues
   - 点击 "New Issue"
   - 描述问题和复现步骤
   - 附上诊断报告

**请提供以下信息：**
- 机型和 BIOS 版本
- Windows 版本
- 小吧控制台版本
- 问题截图
- 诊断报告（如果可以生成）

---

## 更多帮助

- [快速开始指南](QUICKSTART.md)
- [兼容性列表](COMPATIBILITY.md)
- [GitHub Issues](https://github.com/FengXi7420/Xiaoba-Console-Releases/issues)
- [README](../README.md)
