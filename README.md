# OTEL Trace Analysis MCP Server

MCP server for analyzing OpenTelemetry traces with performance and error diagnosis.

## Features

- Load traces from files, strings, or AWS X-Ray
- Auto-detect format (OTLP JSON, Jaeger, Protobuf, X-Ray)
- Performance analysis: latency breakdown, slow spans, critical path
- Error analysis: error detection, exception extraction, context
- MCP sampling for LLM-assisted deep analysis

## Installation

```bash
uv sync
```

## Usage

Run the server:

```bash
uv run otel-mcp
```

Or add to your MCP client config:

```json
{
  "mcpServers": {
    "otel-mcp": {
      "command": "uv",
      "args": ["--directory", "/path/to/otel-mcp", "run", "otel-mcp"]
    }
  }
}
```

## Tools

| Tool | Description |
|------|-------------|
| `load_trace` | Load from file path, JSON string, or X-Ray trace ID |
| `search_xray` | Search X-Ray with filter expressions |
| `list_traces` | List all loaded traces |
| `analyze_perf` | Performance analysis (latency, slow spans, critical path) |
| `analyze_errs` | Error analysis (errors, exceptions, context) |
| `summarize_trace` | High-level trace overview |
| `deep_analyze` | LLM-assisted analysis via MCP sampling |

## Examples

Load a trace file:

```
load_trace(path="/path/to/trace.json")
```

Search X-Ray:

```
search_xray(filter_expression='service("my-api") AND responseTime > 5', region="us-east-1")
```

Analyze performance:

```
analyze_perf(trace_id="abc123")
```
