# 🦜️🔗 LangChain ACE (Agentic Context Engineering)

This repository contains a package with Agentic Context Engineering (ACE) enabled as middleware for LangChain v1 [langchain-ace](https://pypi.org/project/langchain-ace/).

Agentic Context Engineering (ACE) is a technique developed at Stanford that enables agents to self-improve, treating context as an evolving playbook.  This playbook accumulates and refines strategies through a process of reflection and curation.

More details from the Stanford paper here: Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models

With ACE as middelware, one can easily enable any agent to use ACE with a simple parameter [ace] parameter:

agent: Any = create_agent(
    model="gpt-4.1",
    tools=[calculator],
    middleware=[ace],
    checkpointer=checkpointer,
)

This ACE middelware implements implements the following:

A reflector that analyzes agent response correctness, reasoning trajectories, and tags playbook bullets as helpful/harmful
A curator that periodically adds new insights to the playbook based on reflections
These entities work in the background using wrappers and hooks provided by LangChain v1’s middleware.
