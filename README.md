[![official JetBrains project](http://jb.gg/badges/incubator-flat-square.svg)](https://github.com/JetBrains#jetbrains-on-github)
# JetBrains MCP Proxy Server

The server proxies requests from client to JetBrains IDE.

## Install MCP Server plugin

https://plugins.jetbrains.com/plugin/26071-mcp-server

## Usage with Claude Desktop

To use this with Claude Desktop, add the following to your `claude_desktop_config.json`.
The full path on MacOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`, on Windows: `%APPDATA%/Claude/claude_desktop_config.json`, on Linux `~/.config/Claude/claude_desktop_config.json`.

```json
{
  "mcpServers": {
    "jetbrains": {
      "command": "npx",
      "args": ["-y", "@rosite/mcp-proxy"]
    }
  }
}
```

## Configuration

If you're running multiple IDEs with MCP server and want to connect to the specific one, add to the MCP server configuration:
```json
"env": {
  "IDE_PORT": "<port of IDE's built-in webserver>",
  "TOOL_PREFIX": "<prefix>_"
}
```
The IDE_PORT can be changed in Settings > Build, Execution, Deployment > Debugger.
```json
"phpstorm": {
  "command": "npx",
  "args": ["-y", "@rosite/mcp-proxy"],
  "env": {
    "IDE_PORT": "63342",
    "TOOL_PREFIX": "phpstorm_"
  }
},
"webstorm": {
  "command": "npx",
  "args": ["-y", "@rosite/mcp-proxy"],
  "env": {
    "IDE_PORT": "63343",
    "TOOL_PREFIX": "webstorm_"
  }
}
```


By default, we connect to IDE on  127.0.0.1 but you can specify a different address/host:
```json
"env": {
  "HOST": "<host/address of IDE's built-in webserver>"
}
```

To enable logging add:
```json
"env": {
  "LOG_ENABLED": "true"
}
```

## How to build
1. Tested on macOS
2. `brew install node pnpm`
3. Run `pnpm build` to build the project
