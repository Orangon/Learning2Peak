# 为 Windows 右键添加 VS Code 快捷打开方式

本文介绍如何在 Windows 右键菜单中添加使用 VS Code 快速打开文件和文件夹的方法。

## 方法一：重新安装 VS Code（推荐）

1. 下载最新的 VS Code 安装包
2. 运行安装程序时，确保勾选"**将'通过Code 打开'操作添加到Windows资源管理器上下文菜单**"选项
3. 完成安装后即可在右键菜单中看到 VS Code 选项

## 方法二：修改注册表

如果你不想重新安装，可以通过修改注册表手动添加：

### 操作步骤：

1. **打开注册表编辑器**
   - 按 `Win + R` 键，输入 `regedit`，回车

2. **为文件夹添加右键菜单**
   - 导航到：`HKEY_CLASSES_ROOT\Directory\shell`
   - 在 `shell` 上右键 → 新建 → 项，命名为 `VSCode`
   - 在右侧窗口双击"默认"，输入显示的名称，如"通过VS Code打开"
   - 在 `VSCode` 上右键 → 新建 → 项，命名为 `command`
   - 在右侧窗口双击"默认"，输入 VS Code 的安装路径：
     ```
     "C:\Users\你的用户名\AppData\Local\Programs\Microsoft VS Code\Code.exe" "%V"
     ```

3. **为文件添加右键菜单**
   - 导航到：`HKEY_CLASSES_ROOT\*\shell`
   - 重复上述步骤 2 的操作

4. **为文件夹空白处添加右键菜单**
   - 导航到：`HKEY_CLASSES_ROOT\Directory\Background\shell`
   - 重复上述步骤 2 的操作


### 常见 VS Code 安装路径：
- `C:\Users\用户名\AppData\Local\Programs\Microsoft VS Code\Code.exe`
- `C:\Program Files\Microsoft VS Code\Code.exe`

## 方法三：使用注册表文件

创建一个 `.reg` 文件，内容如下：

```reg
Windows Registry Editor Version 5.00

; 右键文件夹用VS Code打开
[HKEY_CLASSES_ROOT\Directory\shell\VSCode]
@="通过VS Code打开"
"Icon"="C:\\Users\\你的用户名\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\Directory\shell\VSCode\command]
@="\"C:\\Users\\你的用户名\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe\" \"%V\""

; 右键文件用VS Code打开
[HKEY_CLASSES_ROOT\*\shell\VSCode]
@="通过VS Code打开"
"Icon"="C:\\Users\\你的用户名\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\*\shell\VSCode\command]
@="\"C:\\Users\\你的用户名\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe\" \"%V\""

; 右键文件夹空白处用VS Code打开当前文件夹
[HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode]
@="通过VS Code打开当前文件夹"
"Icon"="C:\\Users\\你的用户名\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"

[HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode\command]
@="\"C:\\Users\\你的用户名\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe\" \"%V\""
```

将文件保存为 `.reg` 格式，双击运行即可。

**注意**：请根据你的实际 VS Code 安装路径修改上述路径中的用户名部分。

## 三种右键场景说明

以上方法可以实现以下三种右键菜单功能：

1. **右键点击文件夹**：在文件夹上右键，选择"通过VS Code打开"
2. **右键点击文件**：在单个文件上右键，选择"通过VS Code打开"
3. **右键点击空白处**：在文件夹内空白处右键，选择"通过VS Code打开当前文件夹"

## Windows 11 现代模式右键菜单

在 Windows 11 中，右键菜单分为两种模式：

- **现代模式**：右键显示简化菜单，需要点击"显示更多选项"才能看到完整菜单
- **经典模式**：直接显示完整的传统右键菜单

### 方法一：切换到经典模式（推荐）

如果希望始终显示完整右键菜单，可以通过以下方式切换到经典模式：
1. 打开注册表编辑器
2. 导航到：`HKEY_CURRENT_USER\Software\Classes\CLSID`
3. 新建项：`{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}`
4. 在该项下新建项：`InprocServer32`
5. 修改"默认"值为空字符串即可

### 方法二：在现代模式中添加 VS Code 选项

Windows 11 的现代右键菜单系统采用了新的架构，传统的注册表方法无法直接添加到简化菜单中。要让 VS Code 出现在现代模式的简化菜单中，有以下几种方法：

#### 使用第三方工具

1. **Microsoft Store 中的工具**：
   - 搜索 "Custom Context Menu" 或类似应用
   - 这些工具可以帮助将程序添加到现代右键菜单

2. **PowerToys**（微软官方工具）：
   - 从 GitHub 或 Microsoft Store 安装 PowerToys
   - 在设置中寻找右键菜单管理功能
   - 添加 VS Code 到现代菜单

#### 使用快捷键替代

- **Shift + 右键**：直接打开经典模式的完整右键菜单
- **Shift + F10**：同样可以打开经典右键菜单

#### 手动创建 Shell 扩展（高级方法）

对于高级用户，可以通过创建自定义的 Shell 扩展程序来实现，但这种方法需要：
- 编程知识（C++/C#）
- 熟悉 Windows Shell API
- 需要以管理员权限安装扩展

### 推荐方案

对于大多数用户，推荐使用以下方案：

1. **最简单**：使用 `Shift + 右键` 快捷键直接打开完整菜单
2. **一劳永逸**：切换到经典模式（方法一）
3. **保持现代感**：使用 PowerToys 等工具管理现代菜单

## 总结

- **方法一**最简单，适合大多数用户
- **方法二**提供更多自定义选项，可以单独配置不同场景
- **方法三**适合需要批量部署的场景，一次性配置所有右键场景

