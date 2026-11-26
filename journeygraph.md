---
layout: page
title: JourneyGraph
permalink: /journeygraph/
description: >-
  JourneyGraph is an open-source Python command-line tool that compares AI agent behaviour
  across versions: paths, retries, loops, errors, latency and outcomes across all traces.
---

**JourneyGraph is an open-source command-line tool for comparing how an AI agent behaves
across versions.** It reads the trace exports you already have and shows what changed across
all runs: which paths became more common, where retries, loops, errors, latency or cost grew,
and which steps are associated with failed runs.

- Source: [github.com/GermanGerken/journeygraph](https://github.com/GermanGerken/journeygraph)
- Package: [pypi.org/project/journeygraph](https://pypi.org/project/journeygraph/)
- License: Apache-2.0. Python 3.11 or later, no runtime dependencies.
- Runs locally: no account, no API key, no telemetry.

## Try it

```bash
pipx run journeygraph demo --output-dir journeygraph-demo
```

This writes a report from synthetic data to `journeygraph-demo/report.html`. To install:

```bash
python -m pip install journeygraph
```

| You want to | Run |
| --- | --- |
| See recurring paths, loops and failures across many runs | `journeygraph analyze traces.jsonl --output-dir report` |
| Compare a baseline and a candidate release | `journeygraph diff before.jsonl after.jsonl --output-dir diff` |
| Fail CI when agent behaviour regresses | `journeygraph check after.jsonl --rules rules.toml --baseline before.jsonl` |

## Questions

**How do I compare two versions of an LLM agent?**
Export the traces of both versions and compare them as two populations, not one trace at a
time: count path variants, retries and loops, and put a confidence interval on each
difference. `journeygraph diff` does this for two trace exports. The
[agent regression case study](/2026/11/18/agent-regression-case-study/) walks through an
example in which the success rate barely moved while one tool's error rate tripled.

**Why isn't the success rate enough?**
A success rate counts outcomes. It does not show how the agent got there, so more retries,
new loops or a slower path can stay hidden. It also leaves out runs that never record an
outcome.

**Which trace formats does it read?**
Canonical JSON Lines, CSV and optional Parquet are stable inputs. Exports with their own
field names can be described in a small TOML mapping. Presets for Langfuse, LangSmith and
Arize Phoenix exports, and OpenTelemetry OTLP input, are experimental. The repository has
an example for TrustGraph agent sessions.

**Does it send my data anywhere?**
No. The core analysis runs locally and sends nothing.

**Is it the same as journeygraph.xyz?**
No. That is an unrelated company that makes 3D-printed travel models. This JourneyGraph is
an open-source developer tool for AI agent traces.

**Who maintains it?**
[German Gerken](/about/), a data engineer.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "JourneyGraph",
  "description": "Open-source command-line tool that compares AI agent behaviour across versions: paths, retries, loops, errors, latency and outcomes across all traces.",
  "applicationCategory": "DeveloperApplication",
  "operatingSystem": "Any (pure Python)",
  "softwareRequirements": "Python 3.11 or later",
  "softwareVersion": "0.3.0",
  "license": "https://www.apache.org/licenses/LICENSE-2.0",
  "url": "https://germangerken.github.io/journeygraph/",
  "sameAs": ["https://github.com/GermanGerken/journeygraph", "https://pypi.org/project/journeygraph/"],
  "downloadUrl": "https://pypi.org/project/journeygraph/",
  "isAccessibleForFree": true,
  "offers": {"@type": "Offer", "price": "0", "priceCurrency": "USD"},
  "author": {"@type": "Person", "name": "German Gerken", "url": "https://germangerken.github.io/about/"}
}
</script>
