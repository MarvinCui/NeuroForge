# How To: Chown Extra

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate run: Container should change the UID/GID of CHOWN_EXTRA.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `time`
- `pytest`

**Setup Required:**
```python
# Fixtures: container
```

## Step-by-Step Guide

### Step 1: Assign c = container.run(...)

```python
c = container.run(tty=True, user='root', environment=['CONTAINER_UID=1010', 'CONTAINER_GID=101', 'CHOWN_EXTRA=/usr/bin', 'CHOWN_EXTRA_OPTS=-R'], command=['start.sh', 'bash', '-c', "stat -c '%n:%u:%g' /usr/bin/python"])
```


## Complete Example

```python
# Setup
# Fixtures: container

# Workflow
c = container.run(tty=True, user='root', environment=['CONTAINER_UID=1010', 'CONTAINER_GID=101', 'CHOWN_EXTRA=/usr/bin', 'CHOWN_EXTRA_OPTS=-R'], command=['start.sh', 'bash', '-c', "stat -c '%n:%u:%g' /usr/bin/python"])
```

## Next Steps


---

*Source: test_container_options.py:50 | Complexity: Beginner | Last updated: 2026-05-18*