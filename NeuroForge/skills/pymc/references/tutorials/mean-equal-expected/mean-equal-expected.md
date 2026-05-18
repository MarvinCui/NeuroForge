# How To: Mean Equal Expected

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mean equal expected

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
# Fixtures: dist, dist_params, expected
```

## Step-by-Step Guide

### Step 1: Assign expected = np.asarray(...)

```python
expected = np.asarray(expected)
```

### Step 2: Assign rv = dist.dist(...)

```python
rv = dist.dist(**dist_params)
```

### Step 3: Assign mode = Mode(...)

```python
mode = Mode(linker='py', optimizer=None)
```

### Step 4: Assign pymc_mean = mean.eval(...)

```python
pymc_mean = mean(rv).eval(mode=mode)
```

### Step 5: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(pymc_mean, expected)
```

### Step 6: Assign pymc_mean_tiled = mean.eval(...)

```python
pymc_mean_tiled = mean(dist.dist(shape=(3, *pymc_mean.shape), **dist_params)).eval()
```

### Step 7: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(pymc_mean_tiled, np.tile(pymc_mean, (3,) + (1,) * pymc_mean.ndim))
```


## Complete Example

```python
# Setup
# Fixtures: dist, dist_params, expected

# Workflow
expected = np.asarray(expected)
rv = dist.dist(**dist_params)
mode = Mode(linker='py', optimizer=None)
pymc_mean = mean(rv).eval(mode=mode)
np.testing.assert_almost_equal(pymc_mean, expected)
pymc_mean_tiled = mean(dist.dist(shape=(3, *pymc_mean.shape), **dist_params)).eval()
np.testing.assert_almost_equal(pymc_mean_tiled, np.tile(pymc_mean, (3,) + (1,) * pymc_mean.ndim))
```

## Next Steps


---

*Source: test_means.py:253 | Complexity: Intermediate | Last updated: 2026-05-18*