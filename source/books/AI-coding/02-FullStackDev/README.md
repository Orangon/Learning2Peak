# 后端开发

## Mac
Mac通过本地安装小皮面板的方式配置了Mysql。
以这种方式安装的MySQL位置在：`/Applications/phpstudy/Extensions/MySQL5.7.28/bin`
启动命令：`./mysql -u root -p`
要进行备份，需要执行：
````bash
/usr/local/mysql/bin/mysqldump -u 用户名 -p 数据库名 > 导出路径.sql
````
`/Applications/phpstudy/Extensions/MySQL5.7.28/bin/mysqldump -u kitty_user -p cheesepuff_db > cheesepuff_db_backup_$(date +%Y%m%d_%H%M%S).sql`
其中导出的sql地址默认放在当前工作目录下（pwd），也可替换为绝对路径。

# 用uniapp+CC+glm+code buddy编程的最佳实践
preview里面，HTML selection传给IDE的到底是什么？
Chorme Dev tools mcp能实现什么？


# 服务器放行端口

要让外网通过 `IP:端口` 的形式访问到你部署在宝塔面板上的后端服务（5010端口），需要完成以下几个关键步骤：
### 1. **确认服务器IP和端口状态**
- 首先获取服务器的 **公网IP**（不是内网IP，可在云服务商控制台或通过 `curl ifconfig.me` 命令查看）。
- 确保后端服务确实在监听 **0.0.0.0:5010**（而非仅监听本地127.0.0.1），否则外网无法访问。可通过命令检查：
  ```bash
  # 查看5010端口的监听状态
  netstat -tuln | grep 5010
  # 若显示 0.0.0.0:5010 则正确，若为 127.0.0.1:5010 需修改服务配置
  ```

### 2. **开放宝塔面板的端口权限**
宝塔面板默认会限制端口访问，需手动放行5010端口：
1. 在网站-域名管理添加公网IP
2. 在外网映射添加一个5010端口

### 3. **开放服务器的防火墙端口**
除了宝塔的防火墙，服务器本身的系统防火墙（如CentOS的firewalld、Ubuntu的ufw）也需要放行5010端口：
![[Pasted image 20251011164821.png]]
### 4. **测试访问**
后端API地址：
http://82.157.35.56:5010/api/docs/
完成上述配置后，在外网环境（如手机4G网络）通过 `公网IP:5010` 访问，例如：
- 若后端是HTTP服务，可在浏览器访问 `http://你的公网IP:5010`
- 若后端是API服务，可通过 `curl http://你的公网IP:5010` 测试  ```
- 若使用了Nginx反向代理，需确保代理配置正确，且未拦截端口访问。

通过以上步骤，外网即可正常访问你的后端服务。
现在还缺少生产环境的配置文件env

下面要做的：
- [ ] P0 图片上传：添加COS的接口（阿里云、腾讯云）
- [ ] P0 修复更新猫咪信息接口：调试接口（去掉2个必填参数，或者缩略图用一个默认的logo？）
- [ ] P1 运维：服务器后端.env配置文件设置（联通数据库）
- [ ] P1 前端部署：（nginx）看教程，打包list手动上传，然后怎么自动化
- [ ] P2 用户-角色-权限改造：后端增加注册、修改角色的接口，分为普通用户、管理员2种，普通用户仅可查看
- [ ] P1 写一个脚本，将excel导入sql
- [ ] P0 积累好的Prompt和工作流程！
- [ ] 探索context7 chrome dev tools MCP
- [x] 列表样式修复
- [x] 页面占满全屏
- [x] 编辑页数据为空