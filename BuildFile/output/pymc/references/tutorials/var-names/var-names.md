# How To: Var Names

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test var names

## Prerequisites

**Required Modules:**
- `unittest.mock`
- `numpy`
- `pytest`
- `scipy.stats`
- `arviz_base`
- `pytensor.compile`
- `pymc.distributions`
- `pymc.distributions.transforms`
- `pymc.model`
- `pymc.stats.log_density`
- `tests.distributions.test_multivariate`


## Step-by-Step Guide

### Step 1: Assign idata = from_dict(...)

```python
idata = from_dict({'posterior': {'x': np.arange(100).reshape(4, 25)}})
```

**Verification:**
```python
assert res_y1 is not idata
```

### Step 2: Assign res_y1 = compute_log_likelihood(...)

```python
res_y1 = compute_log_likelihood(idata, var_names=['y1'], extend_inferencedata=False, model=m, progressbar=False)
```

**Verification:**
```python
assert set(res_y1.data_vars) == {'y1'}
```

### Step 3: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(res_y1['y1'].values, st.norm.logpdf([0, 1, 2], np.arange(100)[:, None]).reshape(4, 25, 3))
```

**Verification:**
```python
assert res_y2 is not idata
```

### Step 4: Assign res_y2 = compute_log_likelihood(...)

```python
res_y2 = compute_log_likelihood(idata, var_names=['y2'], extend_inferencedata=False, model=m, progressbar=False)
```

**Verification:**
```python
assert set(res_y2.data_vars) == {'y2'}
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(res_y2['y2'].values, st.norm.logpdf([3, 4], np.arange(100)[:, None]).reshape(4, 25, 2))
```

**Verification:**
```python
assert res_both is idata
```

### Step 6: Assign res_both = compute_log_likelihood(...)

```python
res_both = compute_log_likelihood(idata, model=m, progressbar=False)
```

**Verification:**
```python
assert set(res_both.log_likelihood.data_vars) == {'y1', 'y2'}
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(res_y1['y1'].values, res_both.log_likelihood['y1'].values)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(res_y2['y2'].values, res_both.log_likelihood['y2'].values)
```

### Step 9: Assign x = Normal(...)

```python
x = Normal('x')
```

### Step 10: Assign y1 = Normal(...)

```python
y1 = Normal('y1', x, observed=[0, 1, 2])
```

### Step 11: Assign y2 = Normal(...)

```python
y2 = Normal('y2', x, observed=[3, 4])
```


## Complete Example

```python
# Workflow
with Model() as m:
    x = Normal('x')
    y1 = Normal('y1', x, observed=[0, 1, 2])
    y2 = Normal('y2', x, observed=[3, 4])
idata = from_dict({'posterior': {'x': np.arange(100).reshape(4, 25)}})
res_y1 = compute_log_likelihood(idata, var_names=['y1'], extend_inferencedata=False, model=m, progressbar=False)
assert res_y1 is not idata
assert set(res_y1.data_vars) == {'y1'}
np.testing.assert_allclose(res_y1['y1'].values, st.norm.logpdf([0, 1, 2], np.arange(100)[:, None]).reshape(4, 25, 3))
res_y2 = compute_log_likelihood(idata, var_names=['y2'], extend_inferencedata=False, model=m, progressbar=False)
assert res_y2 is not idata
assert set(res_y2.data_vars) == {'y2'}
np.testing.assert_allclose(res_y2['y2'].values, st.norm.logpdf([3, 4], np.arange(100)[:, None]).reshape(4, 25, 2))
res_both = compute_log_likelihood(idata, model=m, progressbar=False)
assert res_both is idata
assert set(res_both.log_likelihood.data_vars) == {'y1', 'y2'}
np.testing.assert_allclose(res_y1['y1'].values, res_both.log_likelihood['y1'].values)
np.testing.assert_allclose(res_y2['y2'].values, res_both.log_likelihood['y2'].values)
```

## Next Steps


---

*Source: test_log_density.py:75 | Complexity: Advanced | Last updated: 2026-05-18*