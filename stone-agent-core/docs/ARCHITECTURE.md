# Stone Agent Core Architecture

Stone Agent Core is the foundation of the Stone automation system.

It provides a generic node-based execution framework that can be reused across many apps and domains.

## High-Level Architecture

```txt
Workflow Definition
        ↓
Workflow Validator
        ↓
Workflow Executor
        ↓
Node Registry
        ↓
Node Execution
        ↓
Execution Logs
        ↓
Final Result
```

## Main Components

## 1. Base Node

A node is the smallest executable unit in Stone.

Every node must describe:

- id
- name
- type
- description
- input schema
- output schema
- config schema
- permission level
- execute function

Example node types:

- trigger
- condition
- skill
- action
- permission
- output

## 2. Node Registry

The registry stores all available nodes.

It allows the system to:

- register nodes
- list nodes
- find a node by name
- validate node input
- expose node metadata to the backend/frontend

The registry should not care about the domain of the node.

## 3. Workflow Executor

The executor runs a workflow.

It is responsible for:

- reading workflow JSON
- finding the first node
- executing nodes in order
- passing output from one node to another
- recording logs
- stopping on failure
- pausing when approval is required

## 4. Permission Model

Some nodes are safe.

Some nodes are risky.

Example safe nodes:

- classify message
- generate draft
- log action

Example risky nodes:

- send message
- delete file
- run terminal command
- move file

The permission model decides whether a node can execute automatically or needs approval.

## 5. Execution Context

Execution context stores temporary data during workflow execution.

Example:

```txt
message_text
sender_name
message_intent
reply_text
permission_decision
approval_status
```

Each node can read from and write to the execution context.

## 6. Logs

Every workflow run should produce logs.

Example:

```txt
Step 1: manual_message_trigger started
Step 1: manual_message_trigger completed
Step 2: classify_message_intent started
Step 2: classify_message_intent completed
Step 3: approval_gate waiting for user approval
```

Logs are important for:

- debugging
- transparency
- trust
- final-year project explanation

## Core Design Rule

The core should be generic.

Good:

```txt
execute_node(node, context)
validate_input(node, input)
register_node(node)
```

Bad:

```txt
send_telegram_message()
reply_to_whatsapp()
summarize_pdf()
```

Domain-specific logic belongs in `stone-node-packs`.

## Dependency Rule

```txt
stone-agent-core
    ↑
    used by
stone-node-packs
    ↑
    used by
stone-builder
```

Stone Agent Core should not import Stone Node Packs.

Stone Node Packs can import Stone Agent Core.

Stone Builder can import both.
