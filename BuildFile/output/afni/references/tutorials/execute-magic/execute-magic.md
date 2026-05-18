# How To: Execute Magic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test calling execute with magic while caching.

## Prerequisites

**Required Modules:**
- `__future__`
- `tempfile`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test calling execute with magic while caching.'

```python
'Test calling execute with magic while caching.'
```

**Verification:**
```python
assert_array_equal(y, y2)
```

### Step 2: Assign x = mdp.numx_rand.rand(...)

```python
x = mdp.numx_rand.rand(100, 10)
```

### Step 3: Assign node = mdp.nodes.PCANode(...)

```python
node = mdp.nodes.PCANode()
```

### Step 4: Assign y = node(...)

```python
y = node(x)
```

### Step 5: Assign y2 = node(...)

```python
y2 = node(x)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(y, y2)
```


## Complete Example

```python
# Workflow
'Test calling execute with magic while caching.'
x = mdp.numx_rand.rand(100, 10)
node = mdp.nodes.PCANode()
with mdp.caching.cache():
    y = node(x)
    y2 = node(x)
    assert_array_equal(y, y2)
```

## Next Steps


---

*Source: test_caching.py:239 | Complexity: Intermediate | Last updated: 2026-05-18*