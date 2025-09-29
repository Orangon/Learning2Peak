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
