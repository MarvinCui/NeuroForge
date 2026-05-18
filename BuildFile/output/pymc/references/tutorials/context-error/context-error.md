# How To: Context Error

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that model_from_fgraph fails when called inside a Model context.

We can't allow it, because the new Model that's returned would be a child of whatever Model context is active.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.graph`
- `pytensor.graph.rewriting.basic`
- `pytensor.tensor.exceptions`
- `pymc`
- `pymc.distributions.shape_utils`
- `pymc.model.fgraph`


## Step-by-Step Guide

### Step 1: "Test that model_from_fgraph fails when called inside a Model context.\n\n    We can't allow it, because the new Model that's returned would be a child of whatever Model context is active.\n    "

```python
"Test that model_from_fgraph fails when called inside a Model context.\n\n    We can't allow it, because the new Model that's returned would be a child of whatever Model context is active.\n    "
```

**Verification:**
```python
assert new_m.parent is None
```

### Step 2: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

**Verification:**
```python
assert x != new_x
```

### Step 3: Assign unknown = fgraph_from_model(...)

```python
fg, _ = fgraph_from_model(m)
```

**Verification:**
```python
assert m.named_vars == {'x': x}
```

### Step 4: Assign new_m = model_from_fgraph(...)

```python
new_m = model_from_fgraph(fg)
```

**Verification:**
```python
assert new_m.named_vars == {'x': new_x}
```

### Step 5: Assign new_x = value

```python
new_x = new_m['x']
```


## Complete Example

```python
# Workflow
"Test that model_from_fgraph fails when called inside a Model context.\n\n    We can't allow it, because the new Model that's returned would be a child of whatever Model context is active.\n    "
with pm.Model() as m:
    x = pm.Normal('x')
    fg, _ = fgraph_from_model(m)
    new_m = model_from_fgraph(fg)
    new_x = new_m['x']
assert new_m.parent is None
assert x != new_x
assert m.named_vars == {'x': x}
assert new_m.named_vars == {'x': new_x}
```

## Next Steps


---

*Source: test_fgraph.py:263 | Complexity: Intermediate | Last updated: 2026-05-18*