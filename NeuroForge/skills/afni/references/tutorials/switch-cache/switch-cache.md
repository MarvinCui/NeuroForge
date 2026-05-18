# How To: Switch Cache

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test changing cache directory while extension is active.

## Prerequisites

**Required Modules:**
- `__future__`
- `tempfile`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test changing cache directory while extension is active.'

```python
'Test changing cache directory while extension is active.'
```

**Verification:**
```python
assert _counter == 1
```

### Step 2: Assign dir1 = tempfile.mkdtemp(...)

```python
dir1 = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
```

**Verification:**
```python
assert _counter == 1
```

### Step 3: Assign dir2 = tempfile.mkdtemp(...)

```python
dir2 = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
```

**Verification:**
```python
assert _counter == 2
```

### Step 4: Assign x = mdp.numx.array(...)

```python
x = mdp.numx.array([[10]], dtype='d')
```

**Verification:**
```python
assert _counter == 2
```

### Step 5: Call mdp.caching.activate_caching()

```python
mdp.caching.activate_caching(cachedir=dir1)
```

### Step 6: Assign node = _CounterNode(...)

```python
node = _CounterNode()
```

### Step 7: Assign _counter = 0

```python
_counter = 0
```

### Step 8: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 1
```

### Step 9: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 1
```

### Step 10: Call mdp.caching.set_cachedir()

```python
mdp.caching.set_cachedir(cachedir=dir2)
```

### Step 11: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 2
```

### Step 12: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 2
```

### Step 13: Call mdp.caching.deactivate_caching()

```python
mdp.caching.deactivate_caching()
```


## Complete Example

```python
# Workflow
'Test changing cache directory while extension is active.'
global _counter
dir1 = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
dir2 = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
x = mdp.numx.array([[10]], dtype='d')
mdp.caching.activate_caching(cachedir=dir1)
node = _CounterNode()
_counter = 0
node.execute(x)
assert _counter == 1
node.execute(x)
assert _counter == 1
mdp.caching.set_cachedir(cachedir=dir2)
node.execute(x)
assert _counter == 2
node.execute(x)
assert _counter == 2
mdp.caching.deactivate_caching()
```

## Next Steps


---

*Source: test_caching.py:209 | Complexity: Advanced | Last updated: 2026-05-18*