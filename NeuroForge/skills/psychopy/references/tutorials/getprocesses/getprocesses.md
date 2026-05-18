# How To: Getprocesses

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: test getProcesses

## Prerequisites

**Required Modules:**
- `psychopy.tests`
- `psychopy.tests.test_iohub.testutil`
- `psychopy.iohub`
- `psychopy.core`


## Step-by-Step Guide


## Complete Example

```python
# Workflow
assert Computer.is_iohub_process is False
assert Computer.psychopy_process == Computer.getCurrentProcess()
assert Computer.current_process == Computer.psychopy_process
assert Computer.iohub_process == Computer.getIoHubProcess()
assert Computer.iohub_process.pid == Computer.iohub_process_id
assert Computer.getCurrentProcess().is_running()
assert Computer.getIoHubProcess().is_running()
assert Computer.getIoHubProcess().parent() == Computer.getCurrentProcess()
```

## Next Steps


---

*Source: test_computer.py:48 | Complexity: Beginner | Last updated: 2026-05-18*