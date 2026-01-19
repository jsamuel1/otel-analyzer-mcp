# OTEL Analyzer MCP Server

MCP server for analyzing OpenTelemetry traces with performance and error diagnosis.

## Features

- Load traces from files, strings, or AWS X-Ray
- Auto-detect format (OTLP JSON, Jaeger, Protobuf, X-Ray)
- Performance analysis: latency breakdown, slow spans, critical path
- Error analysis: error detection, exception extraction, context
- MCP sampling for LLM-assisted deep analysis

## Installation

```bash
uv tool install otel-analyzer-mcp
```

Or for development:

```bash
uv sync
```

## Usage

Run the server:

```bash
otel-analyzer-mcp
```

Or add to your MCP client config:

```json
{
  "mcpServers": {
    "otel-analyzer-mcp": {
      "command": "otel-analyzer-mcp"
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

```text
load_trace(path="/path/to/trace.json")
```

Search X-Ray:

```text
search_xray(filter_expression='service("my-api") AND responseTime > 5', region="us-east-1")
```

Analyze performance:

```text
analyze_perf(trace_id="abc123")
```

## License

MIT
