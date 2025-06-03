# AbletonMCP - Ableton Live 模型上下文协议集成中文教程
[![smithery badge](https://smithery.ai/badge/@ahujasid/ableton-mcp)](https://smithery.ai/server/@ahujasid/ableton-mcp)

AbletonMCP 通过模型上下文协议（MCP）将 Ableton Live 与 Claude AI 连接，使 Claude 能够直接与 Ableton Live 交互和控制。此集成支持通过提示辅助音乐制作、音轨创建和 Live 会话操作。

### 加入社区
MCP官方社群：
提供反馈、获取灵感并在 MCP 基础上构建：[Discord](https://discord.gg/3ZrMyGKnaU)。由 [Siddharth](https://x.com/sidahuj) 制作

我的微信：Hersen_GT   (音乐人，非程序员)
## 功能

- **双向通信**：通过基于套接字的服务器将 Claude AI 连接到 Ableton Live
- **音轨操作**：创建、修改和操作 MIDI 和音频音轨
- **乐器和效果选择**：Claude 可以从 Ableton 库中访问和加载合适的乐器、效果和声音
- **片段创建**：创建和编辑带有音符的 MIDI 片段
- **会话控制**：启动和停止播放、触发片段以及控制传输

## 组件

系统包括两个主要组件：

1. **Ableton 远程脚本** (`Ableton_Remote_Script/__init__.py`)：用于 Ableton Live 的 MIDI 远程脚本，创建套接字服务器以接收和执行命令
2. **MCP 服务器** (`server.py`)：实现模型上下文协议并连接到 Ableton 远程脚本的 Python 服务器

## 安装

### 通过 Smithery 安装

通过 [Smithery](https://smithery.ai/server/@ahujasid/ableton-mcp) 自动安装 Claude Desktop 的 Ableton Live 集成：
1.在Mac终端（terminal）下运行下面的代码

```bash
npx -y @smithery/cli install @ahujasid/ableton-mcp --client claude
```

### 前提条件

- Ableton Live 10 或更高版本
- Python 3.8 或更高版本
- [uv 包管理器](https://astral.sh/uv)

如果使用 Mac，请按以下方式安装 uv：
（安装上面步骤的时候会自动安装，为了不出错，可以再运行一次下方代码）

```
brew install uv
```

否则，请从 [uv 官方网站](https://docs.astral.sh/uv/getting-started/installation/) 安装

⚠️ 在安装 UV 之前不要继续下面步骤

### Claude for Desktop 集成

[观看设置说明视频](https://youtu.be/iJWJqyVuPS8)

1. 转到 Claude > setting > Developer > Edit Config > claude_desktop_config.json，添加以下内容：
   
```json
{
    "mcpServers": {
        "AbletonMCP": {
            "command": "uvx",
            "args": [
                "ableton-mcp"
            ]
        }
    }
}
```

### Cursor 集成

通过 uvx 运行 ableton-mcp，无需永久安装。转到 Cursor 设置 > MCP，粘贴以下命令：

```
uvx ableton-mcp
```

⚠️ 一次仅运行一个 MCP 服务器实例（在 Cursor 或 Claude Desktop 上），不要同时运行两者

### 安装 Ableton 远程脚本

[观看设置说明视频](https://youtu.be/iJWJqyVuPS8)

1. 从此仓库下载 `AbletonMCP_Remote_Script/__init__.py` 文件

2. 将文件夹复制到 Ableton 的 MIDI 远程脚本目录。不同操作系统和版本的路径不同。**以下路径之一应该有效，可能需要查找**：

   **对于 macOS：**
   - 方法 1：转到应用程序 > 右键单击 Ableton Live 应用 → 显示包内容 → 导航至：
     `Contents/App-Resources/MIDI Remote Scripts/`
   - 方法 2：如果第一种方法无效，使用直接路径（将 XX 替换为您的版本号）：
     `/Users/[Username]/Library/Preferences/Ableton/Live XX/User Remote Scripts`
   
   **对于 Windows：**
   - 方法 1：
     `C:\Users\[Username]\AppData\Roaming\Ableton\Live x.x.x\Preferences\User Remote Scripts`
   - 方法 2：
     `C:\ProgramData\Ableton\Live XX\Resources\MIDI Remote Scripts\`
   - 方法 3：
     `C:\Program Files\Ableton\Live XX\Resources\MIDI Remote Scripts\`
   *注意：将 XX 替换为您的 Ableton 版本号（例如，10、11、12）*

4. 在远程脚本目录中创建一个名为 'AbletonMCP' 的文件夹，并将下载的 '__init__.py' 文件粘贴进去

3. 启动 Ableton Live

4. 转到设置/偏好设置 → 链接、速度和 MIDI

5. 在控制表面下拉菜单中选择 "AbletonMCP"

6. 将输入和输出设置为“无”

## 使用

### 启动连接

1. 确保 Ableton Live 中已加载 Ableton 远程脚本
2. 确保在 Claude Desktop 或 Cursor 中配置了 MCP 服务器
3. 当您与 Claude 交互时，连接应自动建立

### 与 Claude 一起使用

在 Claude 上设置好配置文件并在 Ableton 中运行远程脚本后，您将看到一个带有 Ableton MCP 工具的锤子图标。

## 功能

- 获取会话和音轨信息
- 创建和修改 MIDI 和音频音轨
- 创建、编辑和触发片段
- 控制播放
- 从 Ableton 浏览器加载乐器和效果
- 向 MIDI 片段添加音符
- 更改速度和其他会话参数

## 示例命令

以下是您可以要求 Claude 执行的一些示例：

- “创建一首 80 年代合成波音轨” [演示](https://youtu.be/VH9g66e42XA)
- “创建 Metro Boomin 风格的嘻哈节拍”
- “创建一个带有合成贝斯乐器的 MIDI 音轨”
- “为我的鼓添加混响”
- “创建一个包含简单旋律的 4 小节 MIDI 片段”
- “获取当前 Ableton 会话的信息”
- “将 808 鼓架加载到选定音轨”
- “在音轨 1 的片段中添加爵士和弦进程”
- “将速度设置为 120 BPM”
- “播放音轨 2 中的片段”

## 故障排除

- **连接问题**：确保已加载 Ableton 远程脚本，并且在 Claude 上配置了 MCP 服务器
- **超时错误**：尝试简化请求或将其分解为更小的步骤
- **尝试过关闭再打开吗？**：如果仍有连接错误，尝试重启 Claude 和 Ableton Live

## 技术细节

### 通信协议

系统通过 TCP 套接字使用基于 JSON 的简单协议：

- 命令作为 JSON 对象发送，包含 `type` 和可选的 `params`
- 响应为 JSON 对象，包含 `status` 和 `result` 或 `message`

### 限制与安全注意事项

- 创建复杂的音乐编排可能需要分解为较小的步骤
- 该工具设计为与 Ableton 的默认设备和浏览器项目配合使用
- 在进行广泛实验之前始终保存您的工作

## 贡献

欢迎贡献！请随时提交拉取请求。

## 免责声明

这是第三方集成，非 Ableton 官方制作。
