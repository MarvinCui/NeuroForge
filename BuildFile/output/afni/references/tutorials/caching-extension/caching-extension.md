# How To: Caching Extension

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the caching extension is working at the global level.

## Prerequisites

**Required Modules:**
- `__future__`
- `tempfile`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test that the caching extension is working at the global level.'

```python
'Test that the caching extension is working at the global level.'
```

**Verification:**
```python
assert mdp.numx.all(node.execute(x) == x)
```

### Step 2: Assign _counter = 0

```python
_counter = 0
```

**Verification:**
```python
assert _counter == k
```

### Step 3: Assign node = _CounterNode(...)

```python
node = _CounterNode()
```

**Verification:**
```python
assert mdp.get_active_extensions() == ['cache_execute']
```

### Step 4: Assign k = 0

```python
k = 0
```

**Verification:**
```python
assert mdp.numx.all(node.execute(x) == x)
```

### Step 5: Assign _counter = 0

```python
_counter = 0
```

**Verification:**
```python
assert _counter == i + 1
```

### Step 6: Assign cachedir = tempfile.mkdtemp(...)

```python
cachedir = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
```

**Verification:**
```python
assert mdp.get_active_extensions() == []
```

### Step 7: Call mdp.caching.activate_caching()

```python
mdp.caching.activate_caching(cachedir=cachedir)
```

**Verification:**
```python
assert mdp.numx.all(node.execute(x) == x)
```

### Step 8: Call mdp.caching.deactivate_caching()

```python
mdp.caching.deactivate_caching()
```

**Verification:**
```python
assert _counter == k
```

### Step 9: Assign _counter = 0

```python
_counter = 0
```

### Step 10: Assign k = 0

```python
k = 0
```

### Step 11: Assign x = mdp.numx.array(...)

```python
x = mdp.numx.array([[i]], dtype='d')
```

### Step 12: Assign x = mdp.numx.array(...)

```python
x = mdp.numx.array([[i]], dtype='d')
```

### Step 13: Assign x = mdp.numx.array(...)

```python
x = mdp.numx.array([[i]], dtype='d')
```

**Verification:**
```python
assert mdp.numx.all(node.execute(x) == x)
```


## Complete Example

```python
# Workflow
'Test that the caching extension is working at the global level.'
global _counter
_counter = 0
node = _CounterNode()
k = 0
for i in range(3):
    x = mdp.numx.array([[i]], dtype='d')
    for j in range(2):
        k += 1
        assert mdp.numx.all(node.execute(x) == x)
        assert _counter == k
_counter = 0
cachedir = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
mdp.caching.activate_caching(cachedir=cachedir)
assert mdp.get_active_extensions() == ['cache_execute']
for i in range(3):
    x = mdp.numx.array([[i]], dtype='d')
    for _ in range(2):
        assert mdp.numx.all(node.execute(x) == x)
        assert _counter == i + 1
mdp.caching.deactivate_caching()
assert mdp.get_active_extensions() == []
_counter = 0
k = 0
for i in range(3):
    x = mdp.numx.array([[i]], dtype='d')
    for j in range(2):
        k += 1
        assert mdp.numx.all(node.execute(x) == x)
        assert _counter == k
```

## Next Steps


---

*Source: test_caching.py:27 | Complexity: Advanced | Last updated: 2026-05-18*