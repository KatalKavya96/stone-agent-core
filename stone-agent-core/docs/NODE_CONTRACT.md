# Stone Node Contract

Every node in Stone must follow a common contract.

This makes the system extensible and allows different nodes to connect with each other.

## Node Categories

Stone supports these node categories:

- app connector
- trigger
- condition
- skill
- action
- permission
- output

## Common Node Fields

Every node should define:

```txt
name
category
description
input_schema
output_schema
config_schema
permission_level
execute
```

## Field Meaning

## name

Unique node name.

Example:

```txt
generate_reply
approval_gate
send_message_mock
```

## category

The type of node.

Example:

```txt
skill
action
permission
trigger
```

## description

Human-readable explanation of what the node does.

## input_schema

Defines what the node needs to run.

Example:

```json
{
  "message_text": "string",
  "sender_name": "string"
}
```

## output_schema

Defines what the node returns.

Example:

```json
{
  "reply_text": "string",
  "confidence": "number"
}
```

## config_schema

Defines what the user can configure from the frontend.

Example:

```json
{
  "tone": "professional",
  "max_length": 120
}
```

## permission_level

Defines how risky the node is.

Example permission levels:

```txt
safe
approval_required
restricted
```

## execute

The function that runs the node.

It receives input and config, then returns output.

## Example Node

```txt
Node: generate_reply
Category: skill

Input:
- message_text
- sender_name
- intent

Config:
- tone
- max_length

Output:
- reply_text
- confidence
- risk_level

Permission:
safe
```

## Connection Rule

Nodes can connect only when the output of one node can satisfy the input of the next node.

Example valid connection:

```txt
generate_reply output:
- reply_text

send_message_mock input:
- reply_text
```

Example invalid connection:

```txt
classify_message output:
- intent

save_file input:
- file_content
```

Unless there is a mapper node, these should not connect directly.

## First Workflow Nodes

For the first Stone workflow, we need these nodes:

```txt
manual_message_trigger
classify_message_intent
permission_policy_check
generate_reply
approval_gate
send_message_mock
log_action
```
