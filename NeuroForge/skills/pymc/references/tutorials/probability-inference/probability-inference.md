# How To: Probability Inference

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test probability inference

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor.graph.basic`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.op`
- `scipy`
- `pymc`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: func, scipy_func, test_value
```

## Step-by-Step Guide

### Step 1: Assign res = func.eval(...)

```python
res = func(pt.exp(pm.Normal.dist()), test_value).eval()
```

**Verification:**
```python
assert res.shape == ()
```

### Step 2: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(res, expected)
```

**Verification:**
```python
assert res.shape == (2,)
```

### Step 3: Assign res = func.eval(...)

```python
res = func(pt.exp(pm.Normal.dist(size=(2,))), test_value).eval()
```

**Verification:**
```python
assert res.shape == (3, 2)
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(res, expected)
```

### Step 5: Assign res = func.eval(...)

```python
res = func(pt.exp(pm.Normal.dist(size=(2,))), np.broadcast_to(test_value, (3, 2))).eval()
```

**Verification:**
```python
assert res.shape == (3, 2)
```

### Step 6: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(res, expected)
```

### Step 7: Assign expected = np.log1p(...)

```python
expected = np.log1p(-sp.lognorm(s=1).cdf(test_value))
```

### Step 8: Assign expected = getattr(...)

```python
expected = getattr(sp.lognorm(s=1), scipy_func)(test_value)
```


## Complete Example

```python
# Setup
# Fixtures: func, scipy_func, test_value

# Workflow
if scipy_func == 'logccdf':
    expected = np.log1p(-sp.lognorm(s=1).cdf(test_value))
else:
    expected = getattr(sp.lognorm(s=1), scipy_func)(test_value)
res = func(pt.exp(pm.Normal.dist()), test_value).eval()
assert res.shape == ()
np.testing.assert_allclose(res, expected)
res = func(pt.exp(pm.Normal.dist(size=(2,))), test_value).eval()
assert res.shape == (2,)
np.testing.assert_allclose(res, expected)
res = func(pt.exp(pm.Normal.dist(size=(2,))), np.broadcast_to(test_value, (3, 2))).eval()
assert res.shape == (3, 2)
np.testing.assert_allclose(res, expected)
```

## Next Steps


---

*Source: test_basic.py:344 | Complexity: Advanced | Last updated: 2026-05-18*