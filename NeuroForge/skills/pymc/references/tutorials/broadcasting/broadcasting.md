# How To: Broadcasting

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test broadcasting

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.tensor`
- `pytensor.tensor.random`
- `pytensor.tensor.shape`
- `pymc`
- `pymc.distributions.shape_utils`
- `pymc.exceptions`
- `pymc.model`
- `pymc.pytensorf`

**Setup Required:**
```python
# Fixtures: fixture_shapes
```

## Step-by-Step Guide

### Step 1: Assign shapes = fixture_shapes

```python
shapes = fixture_shapes
```

**Verification:**
```python
assert out == expected_out
```

### Step 2: Assign expected_out = value

```python
expected_out = np.broadcast(*(np.empty(s) for s in shapes)).shape
```

### Step 3: Assign out = np.broadcast_shapes(...)

```python
out = np.broadcast_shapes(*shapes)
```

**Verification:**
```python
assert out == expected_out
```

### Step 4: Assign expected_out = None

```python
expected_out = None
```

### Step 5: Call np.broadcast_shapes()

```python
np.broadcast_shapes(*shapes)
```


## Complete Example

```python
# Setup
# Fixtures: fixture_shapes

# Workflow
shapes = fixture_shapes
try:
    expected_out = np.broadcast(*(np.empty(s) for s in shapes)).shape
except ValueError:
    expected_out = None
if expected_out is None:
    with pytest.raises(ValueError):
        np.broadcast_shapes(*shapes)
else:
    out = np.broadcast_shapes(*shapes)
    assert out == expected_out
```

## Next Steps


---

*Source: test_shape_utils.py:91 | Complexity: Advanced | Last updated: 2026-05-18*