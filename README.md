# 🦜️🔗 LangChain Middleware for Agentic Context

Agents can continuously learn when there context is curated and adapted dynamically.
langchain-acm is a package for LangChain v1 middleware that manages agentic context. Currently the package supports Agentic Context Engineering (ACE) developed at Stanford.

**Agentic Context Engineering (ACE)** middleware for LangChain agents that enables self-improvement through evolving playbooks.

[![PyPI version](https://badge.fury.io/py/langchain-acm.svg)](https://badge.fury.io/py/langchain-acm)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

ACE is a technique developed at Stanford that enables agents to self-improve by treating context as an evolving playbook. This playbook accumulates and refines strategies through a process of reflection and curation.

Based on the research paper: [Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models](https://arxiv.org/abs/2510.04618)

This repository contains the `langchain-acm` package in `libs/langchain-acm/`.

## Installation

```bash
pip install langchain-acm
```

## Quick Start

```python
from langchain.agents import create_agent
from ace import ACEMiddleware
from langchain_core.messages import HumanMessage

# Create ACE middleware
ace = ACEMiddleware(
    reflector_model="gpt-4o-mini",
    curator_model="gpt-4o-mini",
    curator_frequency=10,
)

# Create agent with ACE middleware
agent = create_agent(
    model="gpt-4o",
    tools=[calculator],
    middleware=[ace],
)

# The agent will self-improve through playbook evolution
result = agent.invoke({
    "messages": [HumanMessage(content="Calculate the NPV...")]
})
```

## How It Works

The ACE middleware implements a three-role architecture:

| Role | Purpose | When It Runs |
|------|---------|--------------|
| **Generator** | Uses playbook to enhance responses | Every model call |
| **Reflector** | Analyzes trajectories and tags bullets | After each response |
| **Curator** | Adds new insights to playbook | Every N interactions |

## Features

- **Self-improving agents**: Playbook evolves based on what works
- **Fresh bullet protection**: New insights survive at least one evaluation round
- **Token budget enforcement**: Automatic playbook trimming with priority-based selection
- **Ground truth training**: Faster learning when correct answers are available
- **Full tool support**: Works with tool-using agents

## Documentation

See `libs/langchain-acm/README.md` for detailed documentation.

## Quick Start Demo

```bash
cd libs/langchain-acm
export OPENAI_API_KEY="your-key"
uv run python examples/ace_playbook_demo.py
```

## References

- **Paper**: [Agentic Context Engineering](https://arxiv.org/abs/2510.04618)
- **Original Implementation**: [github.com/ace-agent/ace](https://github.com/ace-agent/ace)

## License

MIT License
