## Overview
#### This project provides a simple and intuitive interface to interact with MCP.  
It allows you to spin up an MCP-compatible server, define tools and resources, and test locally with `mcp` CLI or Claude Desktop.

---

## Installation
###Install `uv`

#### Install the `uv` package manager recommended by the MCP documentation:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## Initialize Python project
```bash
uv init
# This automatically generates `pyproject.toml` and sets up a virtual environment
```

## Adding MCP to your python project
#### Documentation recommends installation using `uv`, but also available with `pip`
```bash
uv add "mcp[cli]"
```
```bash
pip installl mcp
```

## Create simple `server.py`

```bash
from mcp.server.fastmcp import FastMCP


# Create an MCP server
mcp = FastMCP("mcp_project") 


# Add an additional tool
@mcp.tool()
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b


# Add a dynamic greeting resource
@mcp.resource("greeting://{name}")
def get_greeting(name: str) -> str:
    """Get a personalized greeting"""
    return f"Hello, {name}!"


if __name__ == "__main__":
    mcp.run()
```

## Virtual environment Notice
#### When installing or using uv, it may automatically create and activate a virtual environment.
#### If you're already inside another virtual environment, make sure to deactivate it to prevent conflicts:
```bash
deactivate
source .venv/bin/activate  #it activates the virtual env of your project
```


## Running Your Server via MCP Inspector
```bash
mcp dev server.py
```

## Install `server.py` on your Claude Desktop
####If the server is running correctly and tools are properly registered, you can install it in Claude Desktop:
```bash
mcp install server.py
```

## Troubleshooting:`uv`path issue
#### If you encounter an error like:
```spawn uv ENONET```
#### It means Claude Desktop cannot find your `uv` binary.

### Solution
#### 1. Find the path to your uv installation:
```bash
which uv
#it may show the path of uv you use
```

#### 2.Modify the `claude_desktop_config.json` to use the full path to `uv`:
```bash
    "mcp_project": {
      "command": "path/to/your/uv", #alter uv into path of uv
      "args": [
        "run",
        "--with",
        "mcp[cli]",
        "mcp",
        "run",
        "/absolute/path/to/your/mcp-server.py"
      ]
    }
  }
}
```
---

## License
#### This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.






