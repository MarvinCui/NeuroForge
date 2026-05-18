# How To: Instance Caching Functionality

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that cached instances really cache.

## Prerequisites

**Required Modules:**
- `__future__`
- `tempfile`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test that cached instances really cache.'

```python
'Test that cached instances really cache.'
```

**Verification:**
```python
assert _counter == 1
```

### Step 2: Assign x = mdp.numx.array(...)

```python
x = mdp.numx.array([[130]], dtype='d')
```

**Verification:**
```python
assert _counter == 2
```

### Step 3: Assign node = _CounterNode(...)

```python
node = _CounterNode()
```

**Verification:**
```python
assert _counter == 1
```

### Step 4: Assign othernode = _CounterNode(...)

```python
othernode = _CounterNode()
```

**Verification:**
```python
assert _counter == 1
```

### Step 5: Assign _counter = 0

```python
_counter = 0
```

### Step 6: Assign _counter = 0

```python
_counter = 0
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
assert _counter == 2
```

### Step 9: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 1
```

### Step 10: Call node.execute()

```python
node.execute(x)
```

**Verification:**
```python
assert _counter == 1
```


## Complete Example

```python
# Workflow
'Test that cached instances really cache.'
global _counter
x = mdp.numx.array([[130]], dtype='d')
node = _CounterNode()
othernode = _CounterNode()
_counter = 0
with mdp.caching.cache(cache_instances=[othernode]):
    node.execute(x)
    assert _counter == 1
    node.execute(x)
    assert _counter == 2
_counter = 0
with mdp.caching.cache(cache_instances=[node]):
    node.execute(x)
    assert _counter == 1
    node.execute(x)
    assert _counter == 1
```

## Next Steps


---

*Source: test_caching.py:165 | Complexity: Advanced | Last updated: 2026-05-18*