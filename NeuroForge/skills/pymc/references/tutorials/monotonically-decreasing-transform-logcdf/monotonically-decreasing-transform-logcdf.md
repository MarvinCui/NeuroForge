# How To: Monotonically Decreasing Transform Logcdf

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test logcdf for monotonically decreasing transforms (Erfc, Erfcx).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.special`
- `pytensor.graph.basic`
- `pymc.distributions.continuous`
- `pymc.distributions.discrete`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.distributions.test_transform`

**Setup Required:**
```python
# Fixtures: pt_transform, transform
```

## Step-by-Step Guide

### Step 1: 'Test logcdf for monotonically decreasing transforms (Erfc, Erfcx).'

```python
'Test logcdf for monotonically decreasing transforms (Erfc, Erfcx).'
```

### Step 2: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal(0.5, 1, name='base_rv')
```

### Step 3: Assign rv = pt_transform(...)

```python
rv = pt_transform(base_rv)
```

### Step 4: Assign vv = rv.clone(...)

```python
vv = rv.clone()
```

### Step 5: Assign rv_logcdf = logcdf(...)

```python
rv_logcdf = logcdf(rv, vv)
```

### Step 6: Assign expected_logcdf = logccdf(...)

```python
expected_logcdf = logccdf(base_rv, transform.backward(vv))
```

### Step 7: Assign vv_test = np.array(...)

```python
vv_test = np.array(0.25)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(rv_logcdf.eval({vv: vv_test}), expected_logcdf.eval({vv: vv_test}))
```


## Complete Example

```python
# Setup
# Fixtures: pt_transform, transform

# Workflow
'Test logcdf for monotonically decreasing transforms (Erfc, Erfcx).'
base_rv = pt.random.normal(0.5, 1, name='base_rv')
rv = pt_transform(base_rv)
vv = rv.clone()
rv_logcdf = logcdf(rv, vv)
expected_logcdf = logccdf(base_rv, transform.backward(vv))
vv_test = np.array(0.25)
np.testing.assert_allclose(rv_logcdf.eval({vv: vv_test}), expected_logcdf.eval({vv: vv_test}))
```

## Next Steps


---

*Source: test_transforms.py:560 | Complexity: Advanced | Last updated: 2026-05-18*