# How To: Unvalued Ir Reversion

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Make sure that un-valued IR rewrites are reverted.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pymc`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: nested
```

## Step-by-Step Guide

### Step 1: 'Make sure that un-valued IR rewrites are reverted.'

```python
'Make sure that un-valued IR rewrites are reverted.'
```

**Verification:**
```python
assert sum((isinstance(node.op, MeasurableOp) for node in z_fgraph.apply_nodes)) == 2
```

### Step 2: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal()
```

### Step 3: Assign y_rv = pt.clip(...)

```python
y_rv = pt.clip(x_rv, 0, 1)
```

### Step 4: Assign z_rv = pt.random.normal(...)

```python
z_rv = pt.random.normal(y_rv, 1, name='z')
```

### Step 5: Assign z_vv = z_rv.clone(...)

```python
z_vv = z_rv.clone()
```

### Step 6: Assign rv_values = value

```python
rv_values = {z_rv: z_vv}
```

### Step 7: Assign z_fgraph = construct_ir_fgraph(...)

```python
z_fgraph = construct_ir_fgraph(rv_values)
```

**Verification:**
```python
assert sum((isinstance(node.op, MeasurableOp) for node in z_fgraph.apply_nodes)) == 2
```

### Step 8: Assign y_rv = value

```python
y_rv = y_rv + 5
```


## Complete Example

```python
# Setup
# Fixtures: nested

# Workflow
'Make sure that un-valued IR rewrites are reverted.'
x_rv = pt.random.normal()
y_rv = pt.clip(x_rv, 0, 1)
if nested:
    y_rv = y_rv + 5
z_rv = pt.random.normal(y_rv, 1, name='z')
z_vv = z_rv.clone()
rv_values = {z_rv: z_vv}
z_fgraph = construct_ir_fgraph(rv_values)
assert sum((isinstance(node.op, MeasurableOp) for node in z_fgraph.apply_nodes)) == 2
```

## Next Steps


---

*Source: test_composite_logprob.py:125 | Complexity: Advanced | Last updated: 2026-05-18*