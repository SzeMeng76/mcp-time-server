# ⏰ MCP 时间服务器

**中文版** | **[English](./README.md)**

> 用于时区管理和时间转换的综合 MCP 服务器

## 🎯 项目概述

一个模型上下文协议（MCP）服务器，提供强大的时区工具，包括跨不同时区的当前时间检索和时区之间的无缝时间转换。使用 TypeScript 构建以确保可靠性，设计为与任何 MCP 兼容客户端配合使用。

## ✨ 功能特性

- 🌍 **全球时区**: 获取世界任何时区的当前时间
- 🔄 **时间转换**: 在不同时区之间精确转换时间
- ⚡ **高性能**: 使用原生 JavaScript API 进行高效时间计算
- 🔧 **TypeScript**: 完整的类型安全和全面的错误处理
- 🌐 **多平台**: 支持本地 MCP 客户端和 Cloudflare Workers
- 📡 **HTTP 支持**: 用于 Web 集成的额外 HTTP 和 SSE 端点
- 🎨 **用户友好**: 清晰、格式化的时间输出和时区信息

## 📦 安装

```bash
npm install mcp-time-server
```

或直接使用 npx：

```bash
npx mcp-time-server
```

## 🔧 配置

### Claude Desktop

```json
{
  "mcpServers": {
    "time": {
      "command": "npx",
      "args": ["mcp-time-server"]
    }
  }
}
```

### Cursor IDE

```json
{
  "mcpServers": {
    "time": {
      "command": "npx",
      "args": ["mcp-time-server"]
    }
  }
}
```

### VS Code 与 GitHub Copilot

```json
{
  "mcp.servers": {
    "time": {
      "command": "npx",
      "args": ["mcp-time-server"],
      "transport": "stdio"
    }
  }
}
```

### 本地开发

```json
{
  "mcpServers": {
    "time": {
      "command": "node",
      "args": ["path/to/mcp-time-server/dist/cli.js"]
    }
  }
}
```

## 🛠️ 可用工具

### `get_current_time`
获取指定时区的当前时间。

**参数：**
- `timezone`（可选）: 时区标识符（如 "America/New_York"、"Asia/Tokyo"、"Europe/London"）
  - 默认：如果未指定则为 "UTC"
  - 支持所有标准 IANA 时区名称

**使用示例：**
```
"东京现在几点了？"
"获取纽约的当前时间"
"显示当前 UTC 时间"
"伦敦现在几点？"
```

**返回内容：**
- 指定时区的格式化日期和时间
- 时区标识符确认
- 24 小时制格式（HH:MM:SS）
- 完整日期（YYYY/MM/DD）

**示例响应：**
```
2025/7/26 14:30:45 (Asia/Tokyo)
```

### `convert_time`
在不同时区之间转换时间。

**参数：**
- `source_timezone`（必需）: 源时区标识符
- `time`（必需）: 要转换的时间，HH:MM 格式（24 小时制）
- `target_timezone`（必需）: 目标时区标识符

**使用示例：**
```
"将 14:30 从东京时间转换为纽约时间"
"伦敦时间 09:00 在洛杉矶是几点？"
"将 18:45 从 UTC 转换为悉尼时间"
```

**返回内容：**
- 原始时间和源时区
- 转换后的时间和目标时区
- 清晰的转换说明

**示例响应：**
```
14:30 在 Asia/Tokyo 相当于 01:30 在 America/New_York
```

## 🎮 使用示例

### 全球业务协调
```
"我们在伦敦、东京和旧金山的办公室现在分别几点？"
"将我们上午 10:00 的会议时间从东部时间转换为所有其他办公室时区"
```

### 旅行规划
```
"如果巴黎是下午 3:00，那么我的目的地曼谷是几点？"
"将我的航班起飞时间 08:30 从洛杉矶时区转换为迪拜到达时区"
```

### 开发和运维
```
"获取用于日志记录的当前 UTC 时间"
"将服务器维护时间 02:00 UTC 转换为所有区域办公室时间"
```

### 调度和协调
```
"将 15:30 中欧时间转换为太平洋标准时间以便我们的团队通话"
"悉尼周一上午 9:00 相当于伦敦几点？"
```

## 🌍 支持的时区

此服务器支持所有标准 IANA 时区标识符，包括：

### 主要地区
- **美洲**: America/New_York、America/Los_Angeles、America/Chicago、America/Toronto
- **欧洲**: Europe/London、Europe/Paris、Europe/Berlin、Europe/Rome
- **亚洲**: Asia/Tokyo、Asia/Shanghai、Asia/Hong_Kong、Asia/Singapore
- **澳大利亚**: Australia/Sydney、Australia/Melbourne、Australia/Perth
- **其他**: UTC、GMT 和所有其他 IANA 时区

### 常见示例
```
UTC                    # 协调世界时
America/New_York       # 美国东部时间
America/Los_Angeles    # 美国太平洋时间
Europe/London          # 格林威治标准时间
Europe/Paris           # 中欧时间
Asia/Tokyo             # 日本标准时间
Asia/Shanghai          # 中国标准时间
Australia/Sydney       # 澳大利亚东部时间
```

## 🏗️ 开发

### 本地设置

```bash
# 克隆仓库
git clone https://github.com/SzeMeng76/mcp-time-server.git
cd mcp-time-server

# 安装依赖
npm install

# 构建项目
npm run build

# 启动服务器
npm start
```

### 项目结构

```
mcp-time-server/
├── src/
│   ├── index.ts          # 主 MCP 服务器实现
│   └── cli.ts            # CLI 和 HTTP 服务器设置
├── dist/                 # 编译后的 JavaScript 文件
├── package.json          # 依赖和脚本
├── tsconfig.json         # TypeScript 配置
└── README.md            # 文档
```

### 核心依赖

- **@modelcontextprotocol/sdk**: 官方 MCP 服务器框架
- **zod**: 运行时类型验证和模式定义
- **http**: 用于 Web 端点的 Node.js HTTP 服务器

## 🔧 技术细节

### 时区处理
- 使用 JavaScript 原生 `Intl.DateTimeFormat` API 进行准确的时区转换
- 支持所有 IANA 时区标识符
- 自动处理夏令时转换
- 提供 24 小时制格式以保持一致性

### 时间转换算法
时间转换过程包含多个步骤以确保准确性：

1. **解析输入时间**: 将 HH:MM 字符串转换为数值
2. **创建本地日期**: 为当前日期构建日期对象
3. **UTC 转换**: 转换为 UTC 作为中间步骤
4. **源验证**: 验证源时区中的输入时间
5. **调整**: 应用时区差异的必要修正
6. **目标格式化**: 在目标时区中格式化结果

### 错误处理
- 对时间格式进行全面的输入验证
- 为无效时区标识符提供清晰的错误消息
- 优雅处理边界情况和夏令时转换
- 使用 Zod 模式进行类型安全的参数处理

### 多平台支持
- **MCP 客户端**: 用于 MCP 兼容性的标准 stdio 传输
- **HTTP 服务器**: 用于 Web 集成的 REST 端点
- **SSE 支持**: 用于实时更新的服务器发送事件
- **Cloudflare Workers**: 云部署支持

## 🌐 HTTP 端点

作为 HTTP 服务器运行时，可使用额外的端点：

### `/mcp`
- **方法**: GET
- **描述**: 服务器状态和可用工具
- **响应**: 包含服务器信息的 JSON

### `/sse`
- **方法**: GET
- **描述**: 服务器发送事件端点
- **响应**: 用于实时更新的事件流

## ⚠️ 重要提示

### 时区准确性
- 所有计算使用官方 IANA 时区数据
- 自动处理夏令时转换
- 对当前日期计算结果准确
- 过去日期可能不反映历史时区变化

### 输入格式
- 时间必须以 24 小时制格式提供（HH:MM）
- 不需要前导零（如 "9:30" 或 "09:30"）
- 输入不支持秒，但输出中显示秒

### 性能考虑
- 时区计算实时执行
- 为保证最大准确性未实施缓存
- 使用高效算法的最小内存占用

## 🚀 常见用例

### 业务运营
- **全球团队**: 跨多个时区协调会议
- **客户支持**: 将支持时间转换为客户当地时间
- **发布管理**: 跨全球基础设施安排部署

### 旅行和物流
- **航班规划**: 在起飞和到达时区之间转换航班时间
- **活动规划**: 安排国际活动和网络研讨会
- **旅行行程**: 在目的地时区规划活动

### 开发和运维
- **日志分析**: 将 UTC 时间戳转换为本地时区
- **监控**: 在适当的区域时区显示警报
- **部署**: 跨区域安排维护窗口

### 个人生产力
- **日历管理**: 为旅行转换约会时间
- **沟通**: 找到跨时区的最佳会议时间
- **规划**: 与国际同事和朋友协调

## 🤝 贡献

1. Fork 仓库
2. 创建功能分支：`git checkout -b feature-name`
3. 使用适当的 TypeScript 类型进行更改
4. 使用各种时区和边界情况进行测试
5. 确保错误处理正常工作
6. 提交带有清晰描述的 pull request

### 开发指南

- 保持 TypeScript 严格模式合规
- 为新功能添加全面的错误处理
- 使用常见和不常见的时区进行测试
- 记录任何新参数或返回格式
- 考虑夏令时边界情况

## 📄 许可证

MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。

## ⚖️ 数据和准确性

- **时区数据**: 使用浏览器/Node.js 内置的 IANA 时区数据库
- **准确性**: 对当前日期和标准转换的计算是准确的
- **更新**: 时区数据随 JavaScript 运行时更新而更新
- **限制**: 可能不完全支持历史时区变化
- **可靠性**: 适用于商业和个人调度应用

## 🙏 致谢

- **IANA**: 维护全面的时区数据库
- **MCP 社区**: 标准化协议
- **JavaScript Intl API**: 强大的国际化支持
- **贡献者**: 所有帮助改进这个项目的人

---

*为全球协调、调度和时区管理而构建* ⏰🌍
