# How To: Different Instances Same Content

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test different instances same content

## Prerequisites

**Required Modules:**
- `__future__`
- `tempfile`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign x = mdp.numx.array(...)

```python
x = mdp.numx.array([[100.0]], dtype='d')
```

**Verification:**
```python
assert _counter == 1
```

### Step 2: Assign cachedir = tempfile.mkdtemp(...)

```python
cachedir = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
```

**Verification:**
```python
assert _counter == 1
```

### Step 3: Call mdp.caching.activate_caching()

```python
mdp.caching.activate_caching(cachedir=cachedir)
```

**Verification:**
```python
assert _counter == 1
```

### Step 4: Assign node = _CounterNode(...)

```python
node = _CounterNode()
```

### Step 5: Assign _counter = 0

```python
_counter = 0
```

### Step 6: Assign node.attr = 'unique'

```python
node.attr = 'unique'
```

### Step 7: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 1
```

### Step 8: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 1
```

### Step 9: Assign _counter = 0

```python
_counter = 0
```

### Step 10: Assign node = _CounterNode(...)

```python
node = _CounterNode()
```

### Step 11: Assign node.attr = 'unique and different'

```python
node.attr = 'unique and different'
```

### Step 12: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 1
```

### Step 13: Call mdp.caching.deactivate_caching()

```python
mdp.caching.deactivate_caching()
```


## Complete Example

```python
# Workflow
global _counter
x = mdp.numx.array([[100.0]], dtype='d')
cachedir = tempfile.mkdtemp(prefix='mdp-tmp-joblib-cache.', dir=py.test.mdp_tempdirname)
mdp.caching.activate_caching(cachedir=cachedir)
node = _CounterNode()
_counter = 0
node.attr = 'unique'
node.execute(x)
assert _counter == 1
node.execute(x)
assert _counter == 1
_counter = 0
node = _CounterNode()
node.attr = 'unique and different'
node.execute(x)
assert _counter == 1
mdp.caching.deactivate_caching()
```

## Next Steps


---

*Source: test_caching.py:73 | Complexity: Advanced | Last updated: 2026-05-18*