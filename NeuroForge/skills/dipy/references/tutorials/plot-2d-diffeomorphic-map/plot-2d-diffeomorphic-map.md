# How To: Plot 2D Diffeomorphic Map

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test plot 2d diffeomorphic map

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy.testing`
- `pytest`
- `dipy.align.imwarp`
- `dipy.align.metrics`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`
- `dipy.viz`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign mv_shape = value

```python
mv_shape = (11, 12)
```

### Step 2: Assign moving = rng.random(...)

```python
moving = rng.random(mv_shape)
```

### Step 3: Assign st_shape = value

```python
st_shape = (13, 14)
```

### Step 4: Assign static = rng.random(...)

```python
static = rng.random(st_shape)
```

### Step 5: Assign dim = value

```python
dim = static.ndim
```

### Step 6: Assign metric = SSDMetric(...)

```python
metric = SSDMetric(dim)
```

### Step 7: Assign level_iters = value

```python
level_iters = [200, 100, 50, 25]
```

### Step 8: Assign sdr = SymmetricDiffeomorphicRegistration(...)

```python
sdr = SymmetricDiffeomorphicRegistration(metric=metric, level_iters=level_iters, inv_iter=50)
```

### Step 9: Assign mapping = sdr.optimize(...)

```python
mapping = sdr.optimize(static, moving)
```

### Step 10: Assign ff = regtools.plot_2d_diffeomorphic_map(...)

```python
ff = regtools.plot_2d_diffeomorphic_map(mapping, delta=10)
```

### Step 11: Call npt.assert_equal()

```python
npt.assert_equal(ff[0].shape, st_shape)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(ff[1].shape, mv_shape)
```

### Step 13: Assign ff = regtools.plot_2d_diffeomorphic_map(...)

```python
ff = regtools.plot_2d_diffeomorphic_map(mapping, delta=10, direct_grid_shape=(7, 8), inverse_grid_shape=(9, 10))
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(ff[0].shape, (7, 8))
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(ff[1].shape, (9, 10))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
mv_shape = (11, 12)
moving = rng.random(mv_shape)
st_shape = (13, 14)
static = rng.random(st_shape)
dim = static.ndim
metric = SSDMetric(dim)
level_iters = [200, 100, 50, 25]
sdr = SymmetricDiffeomorphicRegistration(metric=metric, level_iters=level_iters, inv_iter=50)
mapping = sdr.optimize(static, moving)
ff = regtools.plot_2d_diffeomorphic_map(mapping, delta=10)
npt.assert_equal(ff[0].shape, st_shape)
npt.assert_equal(ff[1].shape, mv_shape)
ff = regtools.plot_2d_diffeomorphic_map(mapping, delta=10, direct_grid_shape=(7, 8), inverse_grid_shape=(9, 10))
npt.assert_equal(ff[0].shape, (7, 8))
npt.assert_equal(ff[1].shape, (9, 10))
```

## Next Steps


---

*Source: test_regtools.py:17 | Complexity: Advanced | Last updated: 2026-05-18*