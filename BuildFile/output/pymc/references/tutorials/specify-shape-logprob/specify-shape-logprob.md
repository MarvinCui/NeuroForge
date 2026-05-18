# How To: Specify Shape Logprob

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test specify shape logprob

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.raise_op`
- `scipy`
- `pymc.distributions`
- `pymc.logprob.basic`
- `tests.distributions.test_multivariate`


## Step-by-Step Guide

### Step 1: Assign last_dim = pt.scalar(...)

```python
last_dim = pt.scalar(name='last_dim', dtype='int64')
```

### Step 2: Assign x_base = Dirichlet.dist(...)

```python
x_base = Dirichlet.dist(pt.ones((last_dim,)), shape=(5, last_dim))
```

### Step 3: Assign x_base.name = 'x'

```python
x_base.name = 'x'
```

### Step 4: Assign x_rv = pt.specify_shape(...)

```python
x_rv = pt.specify_shape(x_base, shape=(5, 3))
```

### Step 5: Assign x_rv.name = 'x'

```python
x_rv.name = 'x'
```

### Step 6: Assign x_vv = x_rv.clone(...)

```python
x_vv = x_rv.clone()
```

### Step 7: Assign unknown = conditional_logp.values(...)

```python
[x_logp] = conditional_logp({x_rv: x_vv}).values()
```

### Step 8: Assign x_logp_fn = pytensor.function(...)

```python
x_logp_fn = pytensor.function([last_dim, x_vv], x_logp)
```

### Step 9: Assign x_vv_test = stats.dirichlet.rvs(...)

```python
x_vv_test = stats.dirichlet(np.ones((3,))).rvs(size=(5,))
```

### Step 10: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(x_logp_fn(last_dim=3, x=x_vv_test), dirichlet_logpdf(x_vv_test, np.ones((3,))))
```

### Step 11: Assign x_vv_test_invalid = stats.dirichlet.rvs(...)

```python
x_vv_test_invalid = stats.dirichlet(np.ones((1,))).rvs(size=(5,))
```

### Step 12: Call x_logp_fn()

```python
x_logp_fn(last_dim=1, x=x_vv_test_invalid)
```


## Complete Example

```python
# Workflow
last_dim = pt.scalar(name='last_dim', dtype='int64')
x_base = Dirichlet.dist(pt.ones((last_dim,)), shape=(5, last_dim))
x_base.name = 'x'
x_rv = pt.specify_shape(x_base, shape=(5, 3))
x_rv.name = 'x'
x_vv = x_rv.clone()
[x_logp] = conditional_logp({x_rv: x_vv}).values()
x_logp_fn = pytensor.function([last_dim, x_vv], x_logp)
x_vv_test = stats.dirichlet(np.ones((3,))).rvs(size=(5,))
np.testing.assert_array_almost_equal(x_logp_fn(last_dim=3, x=x_vv_test), dirichlet_logpdf(x_vv_test, np.ones((3,))))
x_vv_test_invalid = stats.dirichlet(np.ones((1,))).rvs(size=(5,))
with pytest.raises(TypeError, match=re.escape("not compatible with the data's ((5, 1))")):
    x_logp_fn(last_dim=1, x=x_vv_test_invalid)
```

## Next Steps


---

*Source: test_checks.py:51 | Complexity: Advanced | Last updated: 2026-05-18*