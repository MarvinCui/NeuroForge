# How To: Expand Indices Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test expand indices basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.ifelse`
- `pytensor.link.numba`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.shape`
- `pytensor.tensor.subtensor`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.mixture`
- `pymc.logprob.rewriting`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`

**Setup Required:**
```python
# Fixtures: A_parts, indices
```

## Step-by-Step Guide

### Step 1: Assign A = pt.stack(...)

```python
A = pt.stack(A_parts)
```

**Verification:**
```python
assert len(full_indices) == A.ndim
```

### Step 2: Assign at_indices = value

```python
at_indices = [as_index_constant(idx) for idx in indices]
```

**Verification:**
```python
assert np.array_equal(res, exp_res)
```

### Step 3: Assign full_indices = expand_indices(...)

```python
full_indices = expand_indices(at_indices, shape_tuple(A))
```

**Verification:**
```python
assert len(full_indices) == A.ndim
```

### Step 4: Assign exp_res = unknown.eval(...)

```python
exp_res = A[indices].eval()
```

### Step 5: Assign res = unknown.eval(...)

```python
res = A[full_indices].eval()
```

**Verification:**
```python
assert np.array_equal(res, exp_res)
```


## Complete Example

```python
# Setup
# Fixtures: A_parts, indices

# Workflow
A = pt.stack(A_parts)
at_indices = [as_index_constant(idx) for idx in indices]
full_indices = expand_indices(at_indices, shape_tuple(A))
assert len(full_indices) == A.ndim
exp_res = A[indices].eval()
res = A[full_indices].eval()
assert np.array_equal(res, exp_res)
```

## Next Steps


---

*Source: test_mixture.py:731 | Complexity: Intermediate | Last updated: 2026-05-18*