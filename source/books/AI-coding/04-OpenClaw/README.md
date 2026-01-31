# OpenClaw Setup

## 1. 快速开始

进入[官网](https://openclaw.ai/)下载应用到本地，然后运行。

注意使用美国的节点科学上网。

如果使用 npm 安装，可能需要使用 `openclaw gateway` 而非 `openclaw onboard`来启动

之后即可使用 `Ctrl C`关闭。

## 2. 接入飞书机器人

参考这位大佬开源出来的教程：

[GitHub](https://github.com/m1heng/clawdbot-feishu?tab=readme-ov-file#%E4%B8%AD%E6%96%87)

[微信推文](https://mp.weixin.qq.com/s/eeG_uca2p-pJ-tLTgqaFQQ)

注意，如果 Windows 如果 openclaw plugins install 失败，报错 spawn npm ENOENT，可以手动安装：

```shell
# 1. 下载插件包（或者直接粘贴 url 到浏览器下载）
curl -O https://registry.npmjs.org/@m1heng-clawd/feishu/-/feishu-0.1.3.tgz

# 2. 从本地安装
openclaw plugins install ./feishu-0.1.3.tgz

# 3. 从本地用 npm 安装
npm install ./feishu-0.1.3.tgz
```
## 3. 赋予联网搜索能力

这里有两种方式，第一种是接入联网搜索 API，另外一种是通过给 Chrome 浏览器增加插件的方式让它来控制浏览器。

1. 添加 Chrome 浏览器扩展：跟着[教程](https://docs.openclaw.ai/tools/chrome-extension)下载扩展到本地，然后加载到 Chrome 中。

2. 开启扩展：浏览器应该会显示：OpenClaw Browser Relay 已经开始调试此浏览器

3. 开启科学上网（因为默认用谷歌搜索引擎）。
