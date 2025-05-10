# CNKS - 中国知网搜索 aka. CNKI Search

## 简介

CNKS是一个用于搜索中国知网并提取引文数据的工具。该系统能够自动化搜索过程，提取文献信息，并以结构化的方式返回结果。

## 系统架构

CNKS基于MCP标准，使用Playwright框架，需配合本地Chrome客户端使用（默认路径："C:\Program Files\Google\Chrome\Application\chrome.exe"），包含以下主要组件：

1. **服务器 (Server.py)**: 
   - 处理来自客户端的请求
   - 按需调用Worker API处理关键词搜索
   - 管理搜索结果缓存

2. **工作模块 (Worker.py)**: 
   - 提供搜索和数据提取API
   - 使用Playwright自动浏览网页
   - 解析和提取引文数据
   - 不再作为独立进程运行，而是由服务器直接调用

3. **客户端 (Client.py)**:
   - 命令行界面，用于发送搜索请求
   - 接收并显示搜索结果

4. **引文处理器 (Citzer.py)**:
   - 解析和格式化引文数据
   - 支持多种引文格式

## MCP实现

### 要求

- uv / uvx

### 安装步骤 (可选)

1. 克隆仓库到本地：
   ```
   git clone https://github.com/bai-z-l/cnks.git
   cd cnks
   ```

2. 安装依赖：
   ```
   pip install -e .
   ```

## 使用方法

### MCP客户端配置 (仅通过了Cursor验证)
```
{
  "mcpServers": {
    "cnks": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\Users\\ptelegion\\1st_cursor_proj\\cnks",
        "run",
        "cnks"
      ]
   }
  }
} 
```
或
```
{
  "mcpServers": {
    "cnks": {
      "command": "uvx",
      "args": [
        "run",
        "cnks"
      ]
   }
  }
} 
```

### 使用客户端发送请求 (仅用于调试)

```
cnks-client "搜索关键词"
```

选项：
- `--timeout SECONDS`: 设置响应超时时间（默认为60秒）

### 直接测试Worker模块 (仅用于调试)

```
cnks-worker-test "搜索关键词"
```

## 配置

可通过以下环境变量进行配置：

- `CACHE_FILE`: 缓存文件路径，默认为 "cache.json"
- `SEARCH_URL`: 搜索URL，默认为中国知网搜索页面

可以创建`.env`文件设置这些环境变量。

# NOTE

The author is one of my friends whose github account "bai-z-l" is in Spammy.
## 许可证

[项目许可证信息]
