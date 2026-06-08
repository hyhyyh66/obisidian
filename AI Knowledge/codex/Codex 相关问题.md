# Codex 使用问题总结

> 记录日期：2026-05-28

---

## 1. 首次对话需重连五次（网络代理问题）

### 问题描述
首次启动 Codex 进行对话时，连接会反复断开，需要重新连接约 **5 次** 后才能正常使用。

### 原因分析
- 根本原因是**网络代理环境**导致的问题
- Codex 默认通过 HTTPS 连接后端服务，但当前网络环境下的代理配置（可能是 HTTP 代理或未正确配置 SSL 代理）导致 HTTPS 握手不稳定
- 代理可能未正确转发 TLS 加密流量，或存在证书验证问题

### 解决方案
1. **确保代理支持 HTTPS 流量转发**：检查代理工具（如 Clash、V2Ray 等）是否正确配置了 HTTPS 代理规则
2. **设置环境变量**：
   ```bash
   set HTTPS_PROXY=http://127.0.0.1:你的代理端口
   set HTTP_PROXY=http://127.0.0.1:你的代理端口
   ```
3. **开启 TUN 模式**：如果使用 Clash Verge 等工具，开启 TUN 模式可让系统级流量走代理
4. **检查防火墙/杀毒软件**：部分安全软件可能拦截未知应用的 HTTPS 流量
5. **重连几次后稳定**：当前现象是重连 5 次左右后连接趋于稳定，可能是代理首次建立连接时有延迟

---

## 2. Codex App 不支持配置 DeepSeek 模型

### 问题描述
Codex 桌面版 App（GUI）目前**不支持自定义配置 DeepSeek 模型**，只能使用默认提供的模型。

### 原因分析
- Codex App 是封装好的图形化客户端，底层模型配置被固化
- App 版本优先集成了 OpenAI 的模型系列，未开放第三方模型接入入口

### 解决方案
使用 **CLI 版本的 Codex** 来接入 DeepSeek 模型：

```bash
# 安装 Codex CLI（如尚未安装）
npm install -g @anthropic/codex-cli
# 或
pip install codex-cli

# 配置 DeepSeek 模型
# 在 CLI 中可以通过配置文件或命令行参数指定模型
codex config set model deepseek-chat
# 或设置 API 端点指向 DeepSeek
codex config set api_base https://api.deepseek.com/v1
```

### 补充说明
- CLI 版本更灵活，支持自定义 API endpoint 和模型参数
- DeepSeek 的 API 兼容 OpenAI 格式，通过修改 `api_base` 即可接入
- 推荐使用 DeepSeek-V3 或 DeepSeek-R1 模型进行编程辅助

---

## 3. Skills 管理问题

### 问题描述
- Codex 的 **Skills 文件必须放在 `C:\Users\<用户名>\.agents\.skills\` 目录下**
- 目前没有方便的技能管理界面，管理多个 Skills 比较麻烦

### 当前机制
- Skills 是预定义的 prompt/指令模板，用于指导 AI 完成特定类型的任务
- Codex 在对话时会自动扫描 `.skills` 文件夹，但**不会自动启用**某个 skill

### 使用技巧
在每次对话时，**手动提示 AI 使用特定的 skill**：

```
请使用 @skill-name 来帮我完成这个任务
```

或者：

```
使用 python-debugger skill，帮我分析这段代码的问题
```

### Skills 目录结构建议
```
C:\Users\yanha\.agents\.skills\
├── python-debugger.md      # Python 调试技能
├── cpp-reviewer.md         # C++ 代码审查技能
├── git-helper.md           # Git 操作辅助
├── obsidian-note.md        # Obsidian 笔记整理
└── README.md               # 各 skill 的说明索引
```

### 建议
- 创建一个 Skill 索引文件，方便快速查看有哪些可用技能
- 将 Skill 文件通过 Git 或云同步备份，防止丢失
- 命名采用功能性命名，便于在对话中快速引用

---

## 4. 建议每次新建项目时在项目文件夹下对话

### 问题描述
Codex 生成的代码文件如果没有指定路径，可能会散落在默认目录下，不便管理。

### 最佳实践
每次开始新项目时，遵循以下流程：

1. **先创建项目文件夹**：
   ```bash
   mkdir my-new-project
   cd my-new-project
   ```

2. **在该文件夹下启动 Codex 对话**：
   ```bash
   codex chat
   # 或 App 中打开该文件夹作为工作区
   ```

3. **让 AI 生成的文件直接落在当前项目目录下**：
   ```
   请在当前目录下创建 xxx.py 文件
   ```
## mcp配置相关注意事项
- 需要拥有python环境，py3.10以上才可以
- 需要在py环境里面按照mcp相关依赖
- 设置里面可以查看已安装mcp，我是让ai自己写的mcp，不好用，我觉得我需要去git hub上下载别人的mcp。
### 好处
- 所有生成的文件集中在项目文件夹内，方便查找和管理
- 避免文件散落在 Desktop 或其他临时目录
- 便于后续用 Git 进行版本控制
- 项目上下文清晰，AI 可以更好地理解项目结构

### 建议的工作流
```
D:\WorkSpace\MyProject\    ← 在这里打开 Codex
├── src/                   ← AI 生成的源码
├── tests/                 ← AI 生成的测试
├── docs/                  ← AI 生成的文档
└── README.md              ← 项目说明
```

---

## 总结

| 问题 | 核心原因 | 解决方案 |
|------|----------|----------|
| 首次对话需重连 5 次 | 代理不支持 HTTPS / TUN 模式未开启 | 开启 TUN 模式或正确配置 HTTPS 代理 |
| App 不支持 DeepSeek | GUI 版本模型配置固化 | 使用 CLI 版本，手动配置 api_base |
| Skills 管理不便 | Skills 必须放在 C 盘固定目录 | 手动在对话中引用，建立索引文件 |
| 文件散落难以管理 | 未在项目目录下对话 | 每次新建项目，在项目文件夹内启动 Codex |