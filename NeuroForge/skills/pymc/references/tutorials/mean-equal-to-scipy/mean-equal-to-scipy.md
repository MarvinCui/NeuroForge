# How To: Mean Equal To Scipy

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mean equal to scipy

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `pytensor.compile.mode`
- `scipy.stats`
- `pymc`
- `pymc.distributions.moments.means`
- `pymc.exceptions`

**Setup Required:**
```python
# Fixtures: dist, scipy_equiv, dist_params, scipy_params
```

## Step-by-Step Guide

### Step 1: Assign rv = dist.dist(...)

```python
rv = dist.dist(**dist_params)
```

**Verification:**
```python
assert np.asarray(pymc_mean).shape == np.asarray(scipy_mean).shape
```

### Step 2: Assign mode = Mode(...)

```python
mode = Mode(linker='py', optimizer=None)
```

### Step 3: Assign pymc_mean = mean.eval(...)

```python
pymc_mean = mean(rv).eval(mode=mode)
```

### Step 4: Assign scipy_rv = scipy_equiv(...)

```python
scipy_rv = scipy_equiv(**scipy_params)
```

**Verification:**
```python
assert np.asarray(pymc_mean).shape == np.asarray(scipy_mean).shape
```

### Step 5: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(pymc_mean, scipy_mean)
```

### Step 6: Assign pymc_mean_tiled = mean.eval(...)

```python
pymc_mean_tiled = mean(dist.dist(shape=(3, *pymc_mean.shape), **dist_params)).eval()
```

### Step 7: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(pymc_mean_tiled, np.tile(pymc_mean, (3,) + (1,) * pymc_mean.ndim))
```

### Step 8: Assign scipy_mean = scipy_rv.mean(...)

```python
scipy_mean = scipy_rv.mean()
```

### Step 9: Assign scipy_mean = value

```python
scipy_mean = scipy_rv.mean
```

### Step 10: Assign scipy_mean = value

```python
scipy_mean = scipy_rv.loc
```


## Complete Example

```python
# Setup
# Fixtures: dist, scipy_equiv, dist_params, scipy_params

# Workflow
rv = dist.dist(**dist_params)
mode = Mode(linker='py', optimizer=None)
pymc_mean = mean(rv).eval(mode=mode)
scipy_rv = scipy_equiv(**scipy_params)
try:
    scipy_mean = scipy_rv.mean()
except TypeError:
    scipy_mean = scipy_rv.mean
except AttributeError:
    scipy_mean = scipy_rv.loc
assert np.asarray(pymc_mean).shape == np.asarray(scipy_mean).shape
np.testing.assert_almost_equal(pymc_mean, scipy_mean)
pymc_mean_tiled = mean(dist.dist(shape=(3, *pymc_mean.shape), **dist_params)).eval()
np.testing.assert_almost_equal(pymc_mean_tiled, np.tile(pymc_mean, (3,) + (1,) * pymc_mean.ndim))
```

## Next Steps


---

*Source: test_means.py:194 | Complexity: Advanced | Last updated: 2026-05-18*