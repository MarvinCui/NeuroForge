# How To: Step Args

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test step args

## Prerequisites

**Required Modules:**
- `logging`
- `unittest.mock`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pytensor`
- `pytensor.compile.ops`
- `xarray`
- `pymc`
- `pymc.backends.ndarray`
- `pymc.distributions`
- `pymc.exceptions`
- `pymc.sampling.mcmc`
- `pymc.stats.convergence`
- `pymc.step_methods`
- `pymc.testing`
- `tests.models`


## Step-by-Step Guide

### Step 1: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(accept(idata0).mean(), 0.5, decimal=1)
```

**Verification:**
```python
assert accept(idata_default).mean() > 0.6
```

### Step 2: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(accept(idata1).mean(), 0.5, decimal=1)
```

### Step 3: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(accept(idata2).mean(), 0.5, decimal=1)
```

### Step 4: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(accept(idata0).mean(), 0.5, decimal=1)
```

### Step 5: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(accept(idata1).mean(), 0.5, decimal=1)
```

### Step 6: Call npt.assert_allclose()

```python
npt.assert_allclose(idata1.sample_stats.scaling, 0)
```

### Step 7: Assign stats = value

```python
stats = idata.sample_stats
```

### Step 8: Assign a = pm.Normal(...)

```python
a = pm.Normal('a')
```

### Step 9: Assign idata_default = pm.sample(...)

```python
idata_default = pm.sample(random_seed=1410)
```

### Step 10: Assign idata0 = pm.sample(...)

```python
idata0 = pm.sample(target_accept=0.5, random_seed=1410)
```

### Step 11: Assign idata1 = pm.sample(...)

```python
idata1 = pm.sample(nuts={'target_accept': 0.5}, random_seed=1410 * 2)
```

### Step 12: Assign idata2 = pm.sample(...)

```python
idata2 = pm.sample(target_accept=0.5, nuts={'max_treedepth': 10}, random_seed=1410)
```

### Step 13: Assign a = pm.Normal(...)

```python
a = pm.Normal('a')
```

### Step 14: Assign b = pm.Poisson(...)

```python
b = pm.Poisson('b', 1)
```

### Step 15: Assign idata0 = pm.sample(...)

```python
idata0 = pm.sample(target_accept=0.5, random_seed=1418)
```

### Step 16: Call pm.sample()

```python
pm.sample(target_accept=0.5, nuts={'target_accept': 0.95}, random_seed=1410)
```

### Step 17: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'invalid value encountered in double_scalars', RuntimeWarning)
```

### Step 18: Assign idata1 = pm.sample(...)

```python
idata1 = pm.sample(nuts={'target_accept': 0.5}, metropolis={'scaling': 0}, random_seed=1418 * 2)
```


## Complete Example

```python
# Workflow
def accept(idata):
    stats = idata.sample_stats
    return stats.acceptance_rate if 'acceptance_rate' in stats else stats.mean_tree_accept
with pm.Model() as model:
    a = pm.Normal('a')
    idata_default = pm.sample(random_seed=1410)
    idata0 = pm.sample(target_accept=0.5, random_seed=1410)
    idata1 = pm.sample(nuts={'target_accept': 0.5}, random_seed=1410 * 2)
    idata2 = pm.sample(target_accept=0.5, nuts={'max_treedepth': 10}, random_seed=1410)
    with pytest.raises(ValueError, match='`target_accept` was defined twice.'):
        pm.sample(target_accept=0.5, nuts={'target_accept': 0.95}, random_seed=1410)
assert accept(idata_default).mean() > 0.6
npt.assert_almost_equal(accept(idata0).mean(), 0.5, decimal=1)
npt.assert_almost_equal(accept(idata1).mean(), 0.5, decimal=1)
npt.assert_almost_equal(accept(idata2).mean(), 0.5, decimal=1)
with pm.Model() as model:
    a = pm.Normal('a')
    b = pm.Poisson('b', 1)
    idata0 = pm.sample(target_accept=0.5, random_seed=1418)
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', 'invalid value encountered in double_scalars', RuntimeWarning)
        idata1 = pm.sample(nuts={'target_accept': 0.5}, metropolis={'scaling': 0}, random_seed=1418 * 2)
npt.assert_almost_equal(accept(idata0).mean(), 0.5, decimal=1)
npt.assert_almost_equal(accept(idata1).mean(), 0.5, decimal=1)
npt.assert_allclose(idata1.sample_stats.scaling, 0)
```

## Next Steps


---

*Source: test_mcmc.py:686 | Complexity: Advanced | Last updated: 2026-05-18*