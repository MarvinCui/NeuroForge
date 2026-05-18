# How To: Check Memory

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check memory

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `shutil`
- `pathlib`
- `pytest`
- `joblib`
- `nilearn`
- `nilearn._utils.cache_mixin`
- `nilearn._utils.helpers`
- `nilearn.datasets.tests.conftest`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign mem_none = Memory(...)

```python
mem_none = Memory(location=None)
```

**Verification:**
```python
assert memory, Memory
```

### Step 2: Assign mem_temp = Memory(...)

```python
mem_temp = Memory(location=str(tmp_path))
```

**Verification:**
```python
assert memory.location == mem_none.location
```

### Step 3: Assign memory = check_memory(...)

```python
memory = check_memory(mem)
```

**Verification:**
```python
assert memory.location == mem_temp.location
```

### Step 4: Assign memory = check_memory(...)

```python
memory = check_memory(mem)
```

**Verification:**
```python
assert memory, Memory
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
mem_none = Memory(location=None)
mem_temp = Memory(location=str(tmp_path))
for mem in [None, mem_none]:
    memory = check_memory(mem)
    assert memory, Memory
    assert memory.location == mem_none.location
for mem in [str(tmp_path), mem_temp]:
    memory = check_memory(mem)
    assert memory.location == mem_temp.location
    assert memory, Memory
```

## Next Steps


---

*Source: test_cache_mixin.py:26 | Complexity: Intermediate | Last updated: 2026-05-18*