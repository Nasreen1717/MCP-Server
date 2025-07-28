# 🧑‍💻 MCP Project Setup Guide (Using uv, mcp, and uvicorn)

**GitHub Link:** [https://github.com/panaversity/learn-agentic-ai/tree/main/03\_ai\_protocols/01\_mcp/04\_fundamental\_%20primitives/01\_hello\_mcp\_server](https://github.com/panaversity/learn-agentic-ai/tree/main/03_ai_protocols/01_mcp/04_fundamental_%20primitives/01_hello_mcp_server)

---

## 📁 Step 1: Open Terminal

Open your system terminal or integrated terminal in VS Code.

---

## 📂 Step 2: Create and Enter the Project Folder

```bash
uv init hello_mcp
cd hello_mcp
```

---

## 📦 Step 3: Install Required Packages

### a. Install MCP Package:

```bash
uv add mcp
```

### b. Install Uvicorn:

```bash
uv add uvicorn
```

### c. Open Project in VS Code:

```bash
code .
```

---

## ⚙️ Step 4: Set the Python Virtual Environment

### a. Locate `.venv` Folder:

* Right-click on `.venv` folder and **copy full path**.

### b. Set Python Interpreter in VS Code:

1. Press `Ctrl + Shift + P` to open Command Palette.
2. Type `Python: Select Interpreter` and select it.
3. Paste the copied path to activate the environment.

---

## 📝 Step 5: Prepare Your `main.py` File

### a. Open `main.py`

### b. Delete all existing code

### c. Add the following MCP server code:

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP(name="hello-mcp", stateless_http=True)
mcp_app = mcp.streamable_http_app()
```

---

## 🚀 Step 6: Run the MCP Server

```bash
uv run uvicorn main:mcp_app
```

### Or with port and hot reload:

```bash
uv run uvicorn main:mcp_app --port 8000 --reload
```

✅ Your MCP server should start successfully.
🔗 Click the URL shown in the terminal to test the server.

---

## 🤖 Step 7: Create and Run a Client Script

### a. Stop the Server

* Press `Ctrl + C` in the terminal to stop the server.

### b. Install `requests` package:

```bash
uv add requests
```

### c. Restart the Server:

```bash
uv run uvicorn main:mcp_app
```

### d. Create a new file `client.py` and add the following code:

```python
import requests

# Define the MCP server URL
url = "http://localhost:8000/mcp/"

# Set the headers to accept JSON and event-stream responses
headers = {
    "Accept": "application/json, text/event-stream",
}

# Create the JSON-RPC request body to list available tools
body = {
    "jsonrpc": "2.0",
    "method": "tools/list",
    "id": 1,
    "params": {},
}

# Send the POST request
response = requests.post(url, headers=headers, json=body)

# Stream and print each line of the response
for line in response.iter_lines():
    if line:
        print(line)
```

### e. Run the Client Script:

```bash
uv run client.py
```

✅ You should see the list of tools printed line-by-line from the MCP server response.

---

### 🏁 Setup Complete — You're now ready to build and test MCP tools!
