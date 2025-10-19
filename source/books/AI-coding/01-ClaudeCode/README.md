# 安装、配置与更新

前置条件：Node.js>=22

## 01安装

打开 PowerShell/终端 运行`npm install -g @anthropic-ai/claude-code`

> 命令解释：@anthropic-ai/claude-code 是一个 Node.js 包，NPM 是包的管理工具，install 表示从网络上寻找并安装包，-g 是 --global 的简称，表示全局安装（不需要每个项目内部再次安装）。

安装之后可以通过运行`claude --version`来查看版本号，从而确定是否安装成功，
或者通过运行`npm list -g`查看全局安装的包是否含有@anthropic-ai/claude-code。

## 02配置

打开.claude.json文件（推荐使用Everything），
添加一行配置：`"hasCompletedOnboarding": true`，表示已经登陆过，这样可以绕过Claude的登录要求。

## 03切换模型

修改环境变量，使 Claude Code 能够使用 GLM 系列模型为默认模型。

请务必将 "你的智谱API Key" 替换为你自己在第一步中获取的真实 API Key。

这里配置了2个模型：GLM-4.6 和 GLM-4.5-air。
> ANTHROPIC_API_KEY: 你的身份凭证。
> 
> ANTHROPIC_BASE_URL: 告诉 Claude Code 将请求发送到智谱的兼容接口，而不是 Anthropic 的官方接口。
> 
> ANTHROPIC_MODEL: 指定要使用的模型。


### Windows

1. 添加永久生效的设置：

```shell
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_BASE_URL", "https://open.bigmodel.cn/api/anthropic", [System.EnvironmentVariableTarget]::User)

[System.Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", "你的智谱API Key", [System.EnvironmentVariableTarget]::User)

[System.Environment]::SetEnvironmentVariable("ANTHROPIC_MODEL", "glm-4.6", [System.EnvironmentVariableTarget]::User)

[System.Environment]::SetEnvironmentVariable("ANTHROPIC_SMALL_FAST_MODEL", "glm-4.5-air", [System.EnvironmentVariableTarget]::User)
```
2. 验证设置生效：

新开一个PowerShell运行`echo $env:ANTHROPIC_BASE_URL`，打印出正确的URL就说明设置生效了。

### Mac OS

1. 确定你使用的 Shell

打开“终端”（Terminal），输入：`echo $SHELL`

如果输出是 /bin/zsh，说明你使用的是 Zsh（macOS Catalina 及以后版本的默认 Shell）。
如果输出是 /bin/bash，说明你使用的是 Bash。

2. 编辑配置文件

以使用 Zsh 为例，在终端中输入：`open -e ~/.zshrc`

这个命令会使用默认的文本编辑器打开配置文件。如果文件不存在，它会自动创建一个。

3. 添加环境变量
在打开的 ~/.zshrc 文件末尾，添加以下三行内容：

```json
# Claude Code: 使用智谱 GLM 模型
export ANTHROPIC_API_KEY="你的智谱API Key"
export ANTHROPIC_BASE_URL="https://open.bigmodel.cn/api/anthropic"
export ANTHROPIC_MODEL="glm-4.6"
export ANTHROPIC_SMALL_FAST_MODEL="glm-4.5-air"
```

注意：如果你使用的是 Bash，请将上述内容添加到 ~/.bash_profile 文件中，编辑命令为 open -e ~/.bash_profile。

4. 应用配置

保存并关闭文本编辑器。回到终端，执行以下命令让刚才的配置立即生效：
`source ~/.zshrc`

（如果你使用的是 Bash，则执行 `source ~/.bash_profile`）
## 04更新

`claude update`

## 05卸载

`npm uninstall -g @anthropic-ai/claude-code`

然后手动删除`.claude`文件夹

# 吴恩达Claude Code课程笔记

## 01
引入
3个例子
## 02 什么是CC？
一个基于CLI的AI编程工具。
和Cursor这种IDE工具相比：
- 交互方式不同
- 通过Agentic Search（即关键词匹配）来读取文件，而不是进行文本嵌入和向量检索。
核心是Memory和Tools。（Grob，Grep）
列举了各种tools，尤其是针对Jupiter Notebook有特别的设计。（应该是为了数据分析专门优化的。）
## 03 设置CC和利用CC理解代码仓库
以RAG系统为例讲解。会列出Todo list。
直接询问：
- 可以询问高层次的问题：仓库的主要内容是什么？
- 询问具体的问题：某个功能实现是什么？
- 要求绘制图表：ASCII图，或者D3.js，还有mermaid图。
- 询问如何运行项目。
- 添加并提交代码。（可以自动生成commit message）

使用/命令：
- /init 初始化本仓库的长期记忆
- /ide 绑定VsCode，可以引用IDE中的文件或者代码
- /# 使用井号（pound key）可以自动添加全局记忆到CLAUDE.md，如always use uv instead pip。
- /help 获得帮助
- /clear 清除对话记录
- /compact 压缩已有的对话记录
- esc 退出现有的进程

CLAUDE.md的三种形态：
1. 存在于项目，由/init生成，与他人共享，且可以在不同子文件夹中存在
2. 存在于项目，被git忽略因而就不与他人共享，包括了个人指令和定制化需求(CLAUDE.local.md)
3. 存在于~/.claude文件夹，被全局引用，仅自己使用
# 04 adding-features新增功能
功能：
1. 引用文件作为上下文：@ tab
2. 开启plan mode： shift tab 2次
3. 截图修改：Mac直接复制粘贴
4. 添加MCP：Claude add mcp playWright（自动截取浏览器图片分析）
# 05 测试、修复、调试和重构
`write tests for xxx think a lot`
pytest
# 06 同时新增多个功能
1. 通过git-worktrees实现并行化：
`git worktree add .trees/xxx-feature` 就可以在.trees文件夹下新建工作树，在写完之后，还可以让CC自动合并worktree并解决冲突。
2. 通过在.claude/commands下面新增md文件，重启后CC可以新增自定义斜杠命令（Slash Commands）。通过输入`/`就能触发。
3. 通过设置settings.local.json，可以默认允许CC操作(/permission-tools)，如：
```json
"permissions":{
	"allow": [
	"Bash(find:*)",
	"Bash(git add:*)",
	"Bash(git commit:*)",
	"mcp_playwright_browser_navigate",
	"mcp_playwright_browser_take_screenshot",
	"Bash(mkdir:*)",
	"Bash(python-mpytest--version)",
	"Bash(uv run:*)",
	"Bash(uv add:*)",
	"Bash(python -m pytest tests/test_ai_generator.py -v)",
	"Bash(python3 -m pytest tests/test_ai_generator.pyv)"
	1,
	"deny":[]
}
```
# 07 集成Github Actions和Hooks

1. 将Claude Code通过Github Actions与仓库连接起来： `/install-github-app`（但是这个我报错：
Install GitHub App                                                                   
Error: Failed to access repository Orangon/Learning2Peak                  
Reason: GitHub Actions setup failed
2. 通过`/hooks`功能，可以在使用工具前、使用工具后、会话开始前、任务结束后等触发命令工具（直接操纵电脑，因此会有警告）。例如`say "hello"`会语音播报“hello”
# 飞书文档资源

https://www.feishu.cn/community/article?id=7525736129069318147

# Claude Code 实践积累

## 01 将常用的命令添加为Slash Commands

我会将常用的Git操作，例如“帮我提交所有修改”、“帮我查看最近的提交记录”等添加为Slash Commands。

## 02 将文档存放在docs文件夹下，并且及时更新

我会将需求文档、设计文档、UI文档等存放在docs文件夹下，并且随着git tag的更新，及时更新文档。

## 03 全局添加MCP

常用的工具：
### Context7

这是一个让AI连接到最新文档信息的MCP工具，[官方网站](https://context7.com/)。在终端配置：
```bash
claude mcp add --transport http context7 https://mcp.context7.com/mcp -s user
```
然后在全局Claude.md中添加一条：
```
When I need code generation, setup or configuration steps, or library/API documentation, always use context7. This means you should automatically use the Context7 MCP tool to parse library IDs and retrieve library documentation, without me having to explicitly request it.
```
即可让大模型自动调用MCP。
例如，查看antd的最新文档，使用tailwind最新样式，学习LangGragh最新文档。
注册之后获取免费的API key可以提高访问速率。
用同样的思路可以把自己的仓库作为文档，给大模型参考，但这需要订阅pro。
```bash
claude mcp add --transport http context7 https://mcp.context7.com/mcp --header "CONTEXT7_API_KEY: 您的API密钥" -s user
```
claude mcp add --transport http context7 https://mcp.context7.com/mcp --header "CONTEXT7_API_KEY: ctx7sk-c093d569-43b8-4549-a08f-56c9402c08e7" -s user
### chrome-devtools
```bash
claude mcp add chrome-devtools npx chrome-devtools-mcp@latest -s user
```
Chrome DevTools MCP 可以从多个环节优化开发流程，尤其适合需要深度调试、自动化测试和性能优化的场景，以下是具体的改进方向和实践方式：


### 1. **自动化重复性调试工作，减少手动操作**
- **场景**：开发中经常需要重复执行“打开页面→点击元素→检查结果”等操作（如表单提交测试、按钮交互验证）。
- **改进方式**：  
  通过 MCP 编写脚本自动完成这些步骤，例如：  
  - 批量测试不同用户角色的登录流程  
  - 自动填充表单并提交，验证后端接口响应  
  - 循环点击分页按钮，检查页面渲染是否正常  
- **优势**：将重复操作转化为可复用的脚本，减少人为操作失误，节省调试时间。


### 2. **深度性能分析与优化闭环**
- **场景**：页面加载慢、交互卡顿，但难以定位具体原因。
- **改进方式**：  
  - 用 MCP 启动性能追踪，获取 LCP（最大内容绘制）、CLS（累积布局偏移）等核心指标  
  - 结合网络请求分析，筛选出耗时超过阈值的接口或资源（如大图片、未压缩的 JS）  
  - 自动执行性能优化方案（如动态加载非关键资源），并通过 MCP 重新测试验证效果  
- **优势**：形成“检测→分析→优化→验证”的闭环，避免凭经验优化的盲目性。


### 3. **跨设备兼容性测试自动化**
- **场景**：需要验证页面在不同设备、网络环境下的表现（如手机端适配、弱网加载）。
- **改进方式**：  
  - 用 MCP 模拟多种设备尺寸（如 iPhone、Android 机型）和网络条件（如 3G、离线）  
  - 自动截取不同场景下的页面截图，对比布局差异  
  - 检测响应式断点是否生效，以及在弱网下是否有合理的加载状态提示  
- **优势**：无需手动切换设备/网络，一键完成多场景测试，覆盖更多边缘情况。


### 4. **实时监控与问题预警**
- **场景**：开发中偶现的错误（如控制台报错、接口超时）难以复现。
- **改进方式**：  
  - 用 MCP 持续监控控制台消息和网络请求，实时捕获错误日志  
  - 当出现特定错误（如 500 状态码、JS 异常）时，自动触发截图和上下文保存（如当前 DOM 结构、 localStorage 数据）  
  - 集成到开发环境中，在代码提交前自动执行监控脚本，提前拦截问题  
- **优势**：将“被动排查”转为“主动监控”，快速定位偶现问题的触发条件。


### 5. **协作效率提升：共享调试上下文**
- **场景**：团队成员间沟通问题时，难以准确描述“复现步骤”和“当前状态”。
- **改进方式**：  
  - 用 MCP 导出当前页面的快照（包括 DOM、网络请求、性能数据），生成可共享的调试报告  
  - 他人可通过 MCP 导入快照，一键还原问题场景，无需重复搭建环境  
  - 结合版本控制，将关键节点的调试数据与代码提交关联，方便追溯历史问题  
- **优势**：减少沟通成本，确保团队成员在同一“调试上下文”中协作。


### 实践建议
- 从高频重复任务入手（如表单测试、性能检测），编写简单脚本验证效果  
- 结合 Chrome 扩展或自定义工具，将 MCP 能力集成到现有开发流程（如 VS Code 插件、CI/CD 管道）  
- 参考 Chrome 官方 MCP 文档中的 API 示例，快速实现具体功能（如页面交互、性能追踪）

### **案例 1：电商网站表单提交的自动化测试**

**场景**：某电商平台有 10+ 种表单（注册、结账、地址修改等），每次迭代后需手动测试所有表单的提交逻辑，耗时且易漏测。

**MCP 解决方案**：

编写脚本实现全流程自动化测试：

1. 用 MCP 打开不同表单页面，自动填充预设的测试数据（含边界值，如超长手机号、特殊字符）
2. 触发提交按钮，通过 MCP 监控网络请求，验证接口返回状态码和响应体
3. 若提交失败，自动截取错误提示截图并记录控制台报错
4. 生成测试报告，标记未通过的用例