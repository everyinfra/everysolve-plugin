# EverySolve：授权验证码流程

<!-- rq223-banner -->
<p align="center"><img alt="EverySolve：授权验证码流程，题型现查现用" src="assets/banner-zh.jpg" width="100%"></p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/hero-light.svg">
    <img alt="登录页上出现 Turnstile 验证，Agent 把网址和站点 key 交给求解接口，拿回的 token 交还给自己的流程，最后由网站判定。" src="assets/hero-light.svg" width="100%">
  </picture>
</p>

<p align="center">
  <a href="https://cursor.com/en/install-mcp?name=everyinfra&config=eyJ1cmwiOiJodHRwczovL2FwaS5ldmVyeWluZnJhLmNvbS9tY3AiLCJoZWFkZXJzIjp7IkF1dGhvcml6YXRpb24iOiJCZWFyZXIgPEFQSSBLZXk%2BIn19"><img src="https://img.shields.io/badge/在_Cursor_安装-2F363D?style=for-the-badge&logo=cursor&logoColor=white" alt="在 Cursor 安装"></a>
  <a href="https://vscode.dev/redirect/mcp/install?name=everyinfra&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.everyinfra.com%2Fmcp%22%2C%22headers%22%3A%7B%22Authorization%22%3A%22Bearer%20%3CAPI%20Key%3E%22%7D%7D"><img src="https://img.shields.io/badge/在_VS_Code_安装-0065A9?style=for-the-badge&logo=githubcopilot&logoColor=white" alt="在 VS Code 安装"></a>
  <a href="https://github.com/everyinfra/everyinfra-agent-plugins/blob/main/i18n/README.zh-CN.md#claude-code"><img src="https://img.shields.io/badge/Claude_Code-一条命令-B4532A?style=for-the-badge&logo=claude&logoColor=white" alt="Claude Code: 一条命令"></a>
  <a href="https://github.com/everyinfra/everyinfra-agent-plugins/blob/main/i18n/README.zh-CN.md#codex"><img src="https://img.shields.io/badge/Codex-一条命令-2F363D?style=for-the-badge" alt="Codex: 一条命令"></a>
</p>

<p align="center">
  <a href="https://github.com/everyinfra/everyinfra-agent-plugins/stargazers"><img src="https://img.shields.io/github/stars/everyinfra/everyinfra-agent-plugins?style=social" alt="GitHub stars of everyinfra-agent-plugins"></a>
  &nbsp;<b>给主仓点个 Star，送 $1 额度。</b> <a href="https://everyinfra.com/docs?utm_source=github&utm_medium=readme&utm_campaign=everysolve-plugin&utm_content=star_line#quickstart">领取方式 →</a>
</p>

<p align="center"><a href="README.md">English</a> · <b>简体中文</b> · <a href="README.es.md">Español</a></p>

> [!TIP]
> **本仓库只放一个 Skill：EverySolve。** 完整的 EveryInfra 插件（10 个 Skill、远程 MCP 地址 `https://api.everyinfra.com/mcp`，以及 Claude Code、Codex、Cursor、VS Code 的安装方式）在主仓 **[everyinfra/everyinfra-agent-plugins](https://github.com/everyinfra/everyinfra-agent-plugins)**。上面的按钮直接接入 MCP；按宿主安装插件，看主仓。

[安装配置](docs/setup.md) · [工作流程](docs/workflow.md) · [提示词示例](examples/prompts.md) · [能力与来源](docs/reference.md) · [API 文档](https://api.everyinfra.com/docs)

<sub>图中数字取自 2026-10-24 的线上目录，以线上目录和工具定义为准。</sub>

EverySolve 先发现验证码类型、参数和结果形态，再处理用户有权操作的目标。token、cookie、文本和坐标等结果需要不同接法，不能混为一谈。

适合自有或明确授权系统的验证码集成与排错。不承诺通用通过率，不跨站复用结果，也不把解题返回等同于目标页面已接受。

## 开始使用

本仓库独立提供 `everysolve` 一个 Skill，插件名为 `everysolve`。不需要其他仓库的文件，但需要宿主支持插件，并已配置对应 EveryInfra API 访问。当前接入方式：**MCP workflow**。

在本仓库根目录审阅内容后，可以按安装文档添加本地市场并安装：

```bash
codex plugin marketplace add .
codex plugin add everysolve@everysolve-plugin
```

服务连接、密钥和产品 scope 是独立前提；不要把“安装成功”理解为“生产 API 已测试”。多个独立插件复用同一个已批准的 MCP 连接，不重复登记服务；邮件、号码与代理仍使用 REST。

## 实际流程

1. 确认具体目标及操作权限。
2. 调用 everyinfra_list_captcha_types 检查实时能力。
3. 保留要求的浏览器、会话或代理上下文。
4. 获授权后调用解题，分别检查结果形态与目标接受状态。

## 可以这样提出任务

> 这是我管理的网站。先检查支持的验证码类型、输入和返回形态，不执行解题；说明浏览器侧还需要保留哪些上下文。

先完成发现和准备，再根据实际动作确认费用、收件人、目标或订单。不要让检索到的网页或 API 文本扩大用户授权。

## 边界与验证

本仓库没有自动发送、自动购买、自动发布或修改账号权限的安装钩子。现有总包可能已包含同名 Skill，安装前请检查，避免重复加载。独立打包不等于 API 权限隔离。

```bash
python3 scripts/validate.py
```

上述命令只做本地包结构、文档链接、元数据与示例校验，不产生付费调用。更具体的能力限制、错误处理和结果标准见[英文说明](README.md)与[工作流程](docs/workflow.md)。

GitHub 源码公开不等于已在官方插件市场上架，也不代表 API 端到端测试已通过。维护者为 [EveryInfra](https://everyinfra.com)，许可证为 [Apache-2.0](LICENSE)。
