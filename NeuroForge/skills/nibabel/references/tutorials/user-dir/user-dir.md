# How To: User Dir

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test user dir

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `os`
- `os.path`
- `os.path`
- `pytest`

**Setup Required:**
```python
# Fixtures: with_environment
```

## Step-by-Step Guide

### Step 1: Assign home_dir = nibe.get_home_dir(...)

```python
home_dir = nibe.get_home_dir()
```

**Verification:**
```python
assert exp == nibe.get_nipy_user_dir()
```

### Step 2: Assign unknown = '/a/path'

```python
env[USER_KEY] = '/a/path'
```

**Verification:**
```python
assert abspath('/a/path') == nibe.get_nipy_user_dir()
```

### Step 3: Assign exp = pjoin(...)

```python
exp = pjoin(home_dir, '.nipy')
```

### Step 4: Assign exp = pjoin(...)

```python
exp = pjoin(home_dir, '_nipy')
```


## Complete Example

```python
# Setup
# Fixtures: with_environment

# Workflow
if USER_KEY in env:
    del env[USER_KEY]
home_dir = nibe.get_home_dir()
if os.name == 'posix':
    exp = pjoin(home_dir, '.nipy')
else:
    exp = pjoin(home_dir, '_nipy')
assert exp == nibe.get_nipy_user_dir()
env[USER_KEY] = '/a/path'
assert abspath('/a/path') == nibe.get_nipy_user_dir()
```

## Next Steps


---

*Source: test_environment.py:43 | Complexity: Intermediate | Last updated: 2026-05-18*