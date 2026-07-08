# Stone Agent Core

Stone Agent Core is the framework layer of the Stone project.

It defines the common system for building, registering, validating, and executing workflow nodes. It is intentionally domain-agnostic. It does not know whether a node is for Telegram, WhatsApp, files, GitHub, IoT, or any other app.

Stone Agent Core only understands the common building blocks:

- Node
- Input
- Output
- Config
- Permission
- Execution
- Logs
- Workflow

## Purpose

The purpose of this repo is to provide the reusable core engine for Stone.

It answers:

- What is a node?
- How is a node registered?
- How is a workflow executed?
- How is input/output validated?
- How are permissions handled?
- How are execution logs generated?
- How are external node packs loaded?

## What This Repo Contains

- Base node contract
- Node registry
- Workflow executor
- Input/output schema structure
- Permission model
- Execution context
- Execution logs
- Extension loading system

## What This Repo Does Not Contain

This repo should not contain:

- Frontend code
- Backend API routes
- Database models
- Telegram-specific logic
- WhatsApp-specific logic
- Gmail-specific logic
- React components
- User dashboard logic

Those belong in other Stone repos.

## Stone Repo Structure

Stone is separated into three main repos:

1. `stone-agent-core`
   - Generic registry and workflow engine.

2. `stone-node-packs`
   - Actual reusable nodes/extensions.

3. `stone-builder`
   - User-facing app with backend, frontend, workflow builder, logs, and approvals.

## Core Rule

Stone Agent Core must remain domain-agnostic.

The core should not care whether a node is:

- `generate_reply`
- `send_telegram_message`
- `read_pdf`
- `fetch_github_issue`
- `check_sensor_data`

Every node should follow the same common contract.

## Basic Flow

```txt
Workflow JSON
    ↓
Workflow Executor
    ↓
Node Registry
    ↓
Node Execution
    ↓
Output + Logs
```

## First Target

The first target of Stone Agent Core is to support this message automation workflow:

```txt
Manual Message Input
→ Classify Message Intent
→ Permission Policy Check
→ Generate Reply
→ Approval Gate
→ Mock Send Message
→ Log Action
```

## Planned Core Modules

```txt
stone_agent_core/
├── base_node.py
├── registry.py
├── executor.py
├── schemas.py
├── permissions.py
├── context.py
├── logs.py
└── loader.py
```

## Development Philosophy

Build the smallest useful core first.

Do not add complex abstractions too early.

Start with:

- one node contract
- one registry
- one executor
- one workflow format
- one working message-reply flow

Then expand.
