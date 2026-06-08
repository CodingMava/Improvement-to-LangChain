## Description
Fixes #7985 

**Problem:** `ToolNode` currently raises a `TypeError` (or incorrectly stringifies) responses from tools that return standard LangChain content block lists (e.g., MCP tools via `langchain-mcp-adapters`).

**Solution:**
Updated `_normalize_tool_response` in `ToolNode` to check if the tool output is a `list` of `dict` objects where the `"type"` aligns with `TOOL_MESSAGE_BLOCK_TYPES`. If valid, the content block list is passed through natively to the `ToolMessage` content without mutation.

**Testing:**
- Added `test_tool_node_mcp_content_blocks` in `test_tool_node.py` to ensure lists are passed through seamlessly.
- Ran all existing prebuilt tests successfully.

## Type of change
- [x] Bug fix (non-breaking change which fixes an issue)
