# Stone Implementation Flow

This document explains the simple implementation order required to reach the first working version of Stone Builder.

## Goal

First working state:

```txt
User opens Stone Builder
→ pastes a message
→ runs workflow
→ gets reply draft
→ approves
→ mock send happens
→ logs are shown
```

---

## Implementation Steps

## 1. Build `stone-agent-core`

- Create the generic engine.
- It should know:
  - what a node is
  - how to register nodes
  - how to execute nodes
  - how to pass data between nodes
  - how to return logs

---

## 2. Test Core With Fake Nodes

- Create very simple test nodes first.
- Example:

```txt
input_text → uppercase_text → log_result
```

- Purpose:
  - confirm core works before building real message nodes.

---

## 3. Build `stone-node-packs`

- Create real nodes for the first message auto-reply flow.

Required nodes:

```txt
manual_message_trigger
classify_message_intent
permission_policy_check
generate_reply
approval_gate
send_message_mock
log_action
```

---

## 4. Test Node Pack Without Backend or Frontend

- Run the whole message flow from terminal.

Flow:

```txt
manual message
→ classify
→ permission check
→ generate reply
→ approval gate
→ mock send
→ log action
```

- Purpose:
  - confirm `stone-agent-core` and `stone-node-packs` work together.

---

## 5. Build `stone-builder` Backend

- Backend imports:

```txt
stone-agent-core
stone-node-packs
```

- Backend exposes APIs:

```txt
GET /nodes
POST /workflow/run
POST /approval/respond
GET /workflow/runs
```

---

## 6. Test Backend With API

- Send workflow JSON to backend.
- Backend runs core + nodes.
- Backend returns:
  - reply draft
  - status
  - logs
  - approval needed or completed

---

## 7. Build `stone-builder` Frontend

- Frontend calls:

```txt
GET /nodes
```

- Frontend shows available nodes as blocks.
- User creates workflow visually.
- Frontend sends workflow JSON to:

```txt
POST /workflow/run
```

---

## 8. Frontend Shows Result

- Show:
  - generated reply
  - approval button
  - logs
  - send/mock-send result

---

# Simple Dependency Chain

```txt
stone-agent-core
        ↓
stone-node-packs
        ↓
stone-builder backend
        ↓
stone-builder frontend
```

---

# First Complete Version

The first complete version of Stone should support this:

```txt
User opens Stone Builder
→ pastes message
→ workflow classifies message
→ workflow checks permission
→ workflow generates reply
→ user approves
→ mock send happens
→ logs are shown
```

---

# Rule

Do not start with WhatsApp, Telegram, mobile app, or real integrations.

Start with:

```txt
manual message input + mock send
```

Then add real app connectors later.
