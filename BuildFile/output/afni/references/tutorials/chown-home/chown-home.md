# How To: Chown Home

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate run: Container should change the CONTAINER_USER home directory owner and 
group to the current value of CONTAINER_UID and CONTAINER_GID.

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
c = container.run(tty=True, user='root', environment=['CONTAINER_UID=1010', 'CONTAINER_GID=101', 'CHOWN_HOME=yes', 'CHOWN_HOME_OPTS=-R'], command=['start.sh', 'bash', '-c', "stat -c '%n:%u:%g' /home/afni_user"])
```


## Complete Example

```python
# Setup
# Fixtures: container

# Workflow
c = container.run(tty=True, user='root', environment=['CONTAINER_UID=1010', 'CONTAINER_GID=101', 'CHOWN_HOME=yes', 'CHOWN_HOME_OPTS=-R'], command=['start.sh', 'bash', '-c', "stat -c '%n:%u:%g' /home/afni_user"])
```

## Next Steps


---

*Source: test_container_options.py:72 | Complexity: Beginner | Last updated: 2026-05-18*