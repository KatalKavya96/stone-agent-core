# Stone Agent Core Roadmap

## Stage 1: Basic Core

Goal:

Create the smallest possible working core.

Tasks:

- Define BaseNode
- Define node categories
- Define input/output/config schema format
- Create NodeRegistry
- Register one mock node
- Execute one node manually

## Stage 2: Workflow Executor

Goal:

Run multiple connected nodes.

Tasks:

- Define workflow JSON format
- Load workflow JSON
- Sort execution order
- Execute nodes one by one
- Pass output through execution context
- Return final result

## Stage 3: Logs

Goal:

Make workflow execution traceable.

Tasks:

- Add execution logs
- Log node start
- Log node success
- Log node failure
- Log approval pause
- Return logs with workflow result

## Stage 4: Permission Model

Goal:

Add safe execution behavior.

Tasks:

- Define permission levels
- Add approval-required nodes
- Pause workflow when approval is needed
- Resume workflow after approval
- Block restricted nodes

## Stage 5: Extension Loading

Goal:

Allow node packs to be loaded externally.

Tasks:

- Define node pack format
- Load nodes from external packages
- Register external nodes
- List loaded node packs

## Stage 6: Stability

Goal:

Make the core reliable.

Tasks:

- Add tests
- Add error handling
- Add schema validation
- Add examples
- Improve documentation
