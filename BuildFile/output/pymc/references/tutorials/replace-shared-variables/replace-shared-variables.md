# How To: Replace Shared Variables

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test replace shared variables

## Prerequisites

**Required Modules:**
- `logging`
- `re`
- `warnings`
- `collections.abc`
- `typing`
- `unittest`
- `jax`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc.exceptions`
- `pymc.sampling.jax`


## Step-by-Step Guide

### Step 1: Assign x = pytensor.shared(...)

```python
x = pytensor.shared(5, name='shared_x')
```

**Verification:**
```python
assert not shared_variables
```

### Step 2: Assign new_x = _replace_shared_variables(...)

```python
new_x = _replace_shared_variables([x])
```

### Step 3: Assign shared_variables = value

```python
shared_variables = [var for var in graph_inputs(new_x) if isinstance(var, SharedVariable)]
```

**Verification:**
```python
assert not shared_variables
```

### Step 4: Assign shared_rng = pytensor.shared(...)

```python
shared_rng = pytensor.shared(np.random.default_rng(), name='shared_rng')
```

### Step 5: Assign x = pytensor.tensor.random.normal(...)

```python
x = pytensor.tensor.random.normal(rng=shared_rng)
```

### Step 6: Call _replace_shared_variables()

```python
_replace_shared_variables([x])
```


## Complete Example

```python
# Workflow
x = pytensor.shared(5, name='shared_x')
new_x = _replace_shared_variables([x])
shared_variables = [var for var in graph_inputs(new_x) if isinstance(var, SharedVariable)]
assert not shared_variables
shared_rng = pytensor.shared(np.random.default_rng(), name='shared_rng')
x = pytensor.tensor.random.normal(rng=shared_rng)
with pytest.raises(ValueError, match='Graph contains shared RandomType variables'):
    _replace_shared_variables([x])
```

## Next Steps


---

*Source: test_jax.py:210 | Complexity: Intermediate | Last updated: 2026-05-18*