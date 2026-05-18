# How To: Categorical Logp Batch Dims

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test categorical logp batch dims

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `itertools`
- `sys`
- `warnings`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.tensor`
- `pymc`
- `pymc.distributions.discrete`
- `pymc.exceptions`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: method
```

## Step-by-Step Guide

### Step 1: Assign p = np.array(...)

```python
p = np.array([0.2, 0.3, 0.5])
```

**Verification:**
```python
assert expr.type.ndim == 0
```

### Step 2: Assign value = np.array(...)

```python
value = np.array(2.0)
```

**Verification:**
```python
assert expr.type.ndim == 1
```

### Step 3: Assign expr = method(...)

```python
expr = method(pm.Categorical.dist(p=p, shape=value.shape), value)
```

**Verification:**
```python
assert expr.type.ndim == 1
```

### Step 4: Assign expected_p = value

```python
expected_p = 0.5 if method is logp else 1.0
```

**Verification:**
```python
assert expr.type.ndim == 1
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(expr.exp().eval(), expected_p)
```

**Verification:**
```python
assert expr.type.ndim == 1
```

### Step 6: Assign bcast_p = value

```python
bcast_p = p[None]
```

### Step 7: Assign batch_value = np.array(...)

```python
batch_value = np.array([0, 1])
```

### Step 8: Assign expr = method(...)

```python
expr = method(pm.Categorical.dist(p=bcast_p, shape=batch_value.shape), batch_value)
```

**Verification:**
```python
assert expr.type.ndim == 1
```

### Step 9: Assign expected_p = value

```python
expected_p = [0.2, 0.3] if method is logp else [0.2, 0.5]
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(expr.exp().eval(), expected_p)
```

### Step 11: Assign expr = method(...)

```python
expr = method(pm.Categorical.dist(p=p, shape=()), batch_value)
```

**Verification:**
```python
assert expr.type.ndim == 1
```

### Step 12: Assign expected_p = value

```python
expected_p = [0.2, 0.3] if method is logp else [0.2, 0.5]
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(expr.exp().eval(), expected_p)
```

### Step 14: Assign batch_p = np.array(...)

```python
batch_p = np.array([p[::-1], p])
```

### Step 15: Assign expr = method(...)

```python
expr = method(pm.Categorical.dist(p=batch_p, shape=batch_value.shape), batch_value)
```

**Verification:**
```python
assert expr.type.ndim == 1
```

### Step 16: Assign expected_p = value

```python
expected_p = [0.5, 0.3] if method is logp else [0.5, 0.5]
```

### Step 17: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(expr.exp().eval(), expected_p)
```

### Step 18: Assign expr = method(...)

```python
expr = method(pm.Categorical.dist(p=batch_p, shape=None), value)
```

**Verification:**
```python
assert expr.type.ndim == 1
```

### Step 19: Assign expected_p = value

```python
expected_p = [0.2, 0.5] if method is logp else [1.0, 1.0]
```

### Step 20: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(expr.exp().eval(), expected_p)
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
p = np.array([0.2, 0.3, 0.5])
value = np.array(2.0)
expr = method(pm.Categorical.dist(p=p, shape=value.shape), value)
assert expr.type.ndim == 0
expected_p = 0.5 if method is logp else 1.0
np.testing.assert_allclose(expr.exp().eval(), expected_p)
bcast_p = p[None]
batch_value = np.array([0, 1])
expr = method(pm.Categorical.dist(p=bcast_p, shape=batch_value.shape), batch_value)
assert expr.type.ndim == 1
expected_p = [0.2, 0.3] if method is logp else [0.2, 0.5]
np.testing.assert_allclose(expr.exp().eval(), expected_p)
expr = method(pm.Categorical.dist(p=p, shape=()), batch_value)
assert expr.type.ndim == 1
expected_p = [0.2, 0.3] if method is logp else [0.2, 0.5]
np.testing.assert_allclose(expr.exp().eval(), expected_p)
batch_p = np.array([p[::-1], p])
expr = method(pm.Categorical.dist(p=batch_p, shape=batch_value.shape), batch_value)
assert expr.type.ndim == 1
expected_p = [0.5, 0.3] if method is logp else [0.5, 0.5]
np.testing.assert_allclose(expr.exp().eval(), expected_p)
expr = method(pm.Categorical.dist(p=batch_p, shape=None), value)
assert expr.type.ndim == 1
expected_p = [0.2, 0.5] if method is logp else [1.0, 1.0]
np.testing.assert_allclose(expr.exp().eval(), expected_p)
```

## Next Steps


---

*Source: test_discrete.py:387 | Complexity: Advanced | Last updated: 2026-05-18*