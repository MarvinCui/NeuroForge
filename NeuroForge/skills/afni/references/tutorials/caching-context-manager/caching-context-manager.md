# How To: Caching Context Manager

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test caching context manager

## Prerequisites

**Required Modules:**
- `__future__`
- `tempfile`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign node = _CounterNode(...)

```python
node = _CounterNode()
```

**Verification:**
```python
assert mdp.get_active_extensions() == []
```

### Step 2: Assign _counter = 0

```python
_counter = 0
```

**Verification:**
```python
assert mdp.get_active_extensions() == ['cache_execute']
```

### Step 3: Assign cachedir = tempfile.mkdtemp(...)

```python
cachedir = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
```

**Verification:**
```python
assert mdp.numx.all(node.execute(x) == x)
```

### Step 4: Assign x = mdp.numx.array(...)

```python
x = mdp.numx.array([[i]], dtype='d')
```

**Verification:**
```python
assert _counter == i + 1
```


## Complete Example

```python
# Workflow
global _counter
node = _CounterNode()
_counter = 0
assert mdp.get_active_extensions() == []
cachedir = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
with mdp.caching.cache(cachedir=cachedir):
    assert mdp.get_active_extensions() == ['cache_execute']
    for i in range(3):
        x = mdp.numx.array([[i]], dtype='d')
        for _ in range(2):
            assert mdp.numx.all(node.execute(x) == x)
            assert _counter == i + 1
assert mdp.get_active_extensions() == []
```

## Next Steps


---

*Source: test_caching.py:104 | Complexity: Intermediate | Last updated: 2026-05-18*