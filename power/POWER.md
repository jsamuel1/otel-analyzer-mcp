---
name: "otel-analyzer"
displayName: "OTEL Analyzer MCP"
description: "Analyze OpenTelemetry traces for performance issues and errors. Load traces from files or AWS X-Ray, get latency breakdowns, find slow spans, identify errors, and use LLM-assisted deep analysis."
keywords: ["opentelemetry", "otel", "traces", "xray", "observability", "performance", "debugging"]
author: "Joshua Samuel"
---

# OTEL Analyzer MCP

## Overview

The OTEL Analyzer MCP server enables AI assistants to analyze OpenTelemetry traces for debugging and performance optimization. Load traces from local files, JSON strings, or directly from AWS X-Ray, then analyze them for performance bottlenecks and errors.

## When to Use This Power

Use the OTEL Analyzer MCP when you need to:

- Analyze distributed traces for performance issues
- Find slow spans and latency bottlenecks
- Identify errors and exceptions in traces
- Query AWS X-Ray for traces matching filter criteria
- Get LLM-assisted deep analysis of complex traces

Do NOT use this power for:

- Collecting or instrumenting traces (use OpenTelemetry SDK)
- Real-time monitoring dashboards
- Metrics or logs analysis (traces only)

## Onboarding

### Prerequisites

- Python 3.11+ with `uv` or `uvx` available
- AWS credentials configured (for X-Ray integration)
- Kiro with MCP Support configured

### Installation

The OTEL Analyzer MCP server is automatically configured when you install this power. No additional installation steps required.

## Tool Selection Guide

| Task | Tool | Example |
|------|------|---------|
| Load trace from file | `load_trace` | "Load trace.json" |
| Load from X-Ray | `load_trace` | "Load X-Ray trace 1-abc123" |
| Search X-Ray traces | `search_xray` | "Find slow traces in us-east-1" |
| List loaded traces | `list_traces` | "What traces are loaded?" |
| Get trace overview | `summarize_trace` | "Summarize this trace" |
| Find slow spans | `analyze_perf` | "Why is this trace slow?" |
| Find errors | `analyze_errs` | "What errors occurred?" |
| Deep analysis | `deep_analyze` | "Explain the root cause" |

## Tools Reference

### load_trace

Load a trace from file, JSON string, or X-Ray trace ID. Auto-detects format (OTLP JSON, Jaeger, Protobuf, X-Ray).

**Parameters**:

- `path` - File path to trace JSON
- `data` - Raw JSON string
- `trace_id` - X-Ray trace ID (e.g., 1-abc123-def456)
- `region` - AWS region for X-Ray (default: us-west-2)
- `profile` - AWS profile name

### search_xray

Search AWS X-Ray for traces matching a filter expression.

**Parameters**:

- `filter_expression` - X-Ray filter (e.g., `service("api") AND responseTime > 5`)
- `region` - AWS region
- `start_time` / `end_time` - Time range
- `limit` - Max results (default: 20)

### analyze_perf

Analyze trace performance: latency breakdown, slow spans, critical path.

**Parameters**:

- `trace_id` - ID of loaded trace
- `slow_threshold_ms` - Threshold for slow span detection

### analyze_errs

Analyze trace errors: error spans, exceptions, failure context.

**Parameters**:

- `trace_id` - ID of loaded trace

### deep_analyze

Use MCP sampling for LLM-assisted trace analysis.

**Parameters**:

- `trace_id` - ID of loaded trace
- `question` - Specific question about the trace

## Common Workflows

### Workflow 1: Analyze Local Trace File

```text
1. "Load the trace from ./traces/slow-request.json"
2. "Summarize this trace"
3. "Why is it slow? Analyze performance"
```

### Workflow 2: Debug X-Ray Traces

```text
1. "Search X-Ray for traces where responseTime > 5 seconds in us-east-1"
2. "Load the slowest trace"
3. "Analyze errors and performance"
```

### Workflow 3: Root Cause Analysis

```text
1. "Load trace 1-abc123-def456 from X-Ray"
2. "What errors occurred in this trace?"
3. "Deep analyze: what's the root cause of the failure?"
```

## X-Ray Filter Expression Examples

```text
service("my-api")
service("my-api") AND responseTime > 5
service("my-api") AND error = true
annotation.user_id = "12345"
http.status = 500
```

## Best Practices

- Load traces before analyzing them
- Use `summarize_trace` first to understand trace structure
- Use `analyze_perf` for latency issues, `analyze_errs` for failures
- Use `deep_analyze` for complex root cause analysis
- Filter X-Ray searches to reduce noise

## Additional Resources

- [OpenTelemetry Documentation](https://opentelemetry.io/docs/)
- [AWS X-Ray Filter Expressions](https://docs.aws.amazon.com/xray/latest/devguide/xray-console-filters.html)
- [GitHub Repository](https://github.com/jsamuel1/otel-analyzer-mcp)

---

**Package**: `otel-analyzer-mcp`
**MCP Server**: `otel-analyzer`
