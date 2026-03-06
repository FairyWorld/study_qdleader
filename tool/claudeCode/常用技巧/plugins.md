# plugins

## 什么是 Plugins?
Plugins 是打包在一起的扩展集合,可以包含:

    5 个 Skills
    10 个斜杠命令
    3 个 MCP 服务器配置
    2 个 SubAgent 定义
    若干 Hooks


## Plugins vs Skills:

特性	Skills	Plugins
复杂度	简单工作流	完整功能套件
内容	单一技能	多种资源的集合
安装	独立安装	一次性安装多个资源
适用场景	单一任务	完整解决方案


## Plugin 安装与使用

### 官方插件市场:
 
 添加官方市场
/plugin 
  -》 add marketplace 
 -》输入 github 地址 https://github.com/anthropics/claude-plugins-official  
 -》 enter 即可



来源	地址	说明
Anthropic Skills	https://github.com/anthropics/skills	官方Skills库,包含多个插件
Claude Code Marketplace	https://claudecodemarketplaces.com	插件市场目录
Awesome Claude Code	https://awesomeclaude.ai/plugins	社区插件精选


## 添加插件市场:

### 添加官方Anthropic插件市场
```js
claude /plugin marketplace add anthropics/skills
```

### 添加本地插件市场
```js
claude /plugin marketplace add ~/my-marketplace
```
### 浏览可用插件
```js
claude /plugin
// # 选择 "Browse Plugins" 查看完整列表
```
常用官方插件:

### 文档处理插件套件
```js
claude /plugin marketplace add anthropics/skills
claude /plugin install document-skills
```
### 前端开发插件
```js
claude /plugin install frontend-design
```

### Git工作流插件
```js
claude /plugin install git-workflow
```


## 安装 Plugin
### 从市场安装:

claude plugin install <plugin-name>


### 从本地安装:
```js
# 安装本地插件
claude plugin install ./my-plugin

# 或使用完整路径
claude plugin install /path/to/my-plugin
从GitHub安装:

# 直接从GitHub仓库安装
claude plugin install github:user/repo
```


查看 Plugins
查看已安装 Plugins:
```js
claude /plugin



浏览可用插件:
# 在Claude Code中输入
/plugin
// # 选择 "Browse Plugins"


```



## 卸载 Plugin:
```js
claude plugin uninstall <plugin-name>
```

### 创建自定义 Plugin:
```js
my-plugin/
├── plugin.json           # Plugin 配置
├── skills/              # Skills 目录
│   ├── skill1/
│   └── skill2/
├── commands/            # 自定义斜杠命令
│   └── my-command.md
├── mcp/                 # MCP 配置
│   └── mcp-config.json
├── agents/              # SubAgent 定义
│   └── agent1.json
└── hooks/               # Hook 脚本
    └── hook1.sh
```

### plugin.json 示例:
```js
{
  "name": "my-plugin",
  "version": "1.0.0",
  "description": "我的自定义插件",
  "author": "Your Name",
  "skills": [
    "skills/skill1"
  ],
  "commands": [
    {
      "name": "/my-command",
      "description": "我的自定义命令",
      "file": "commands/my-command.md"
    }
  ],
  "mcpServers": [
    {
      "name": "my-mcp",
      "config": "mcp/mcp-config.json"
    }
  ],
  "agents": [
    {
      "name": "my-agent",
      "config": "agents/agent1.json"
    }
  ]
}
```