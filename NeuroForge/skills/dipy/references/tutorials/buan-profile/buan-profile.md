# How To: Buan Profile

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test buan profile

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.stats.analysis`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign data = np.ones(...)

```python
data = np.ones((40, 40, 40), dtype=float)
```

### Step 2: Assign n_pts = 20

```python
n_pts = 20
```

### Step 3: Assign x = np.linspace(...)

```python
x = np.linspace(5, 34, n_pts)
```

### Step 4: Assign y0 = 20.0

```python
y0 = 20.0
```

### Step 5: Assign z0 = 20.0

```python
z0 = 20.0
```

### Step 6: Assign base = value

```python
base = np.vstack([x, np.ones(n_pts) * y0, np.ones(n_pts) * z0]).T
```

### Step 7: Assign bundle = Streamlines(...)

```python
bundle = Streamlines([base + np.array([0, i, 0]) for i in range(10)])
```

### Step 8: Assign model_bundle = Streamlines(...)

```python
model_bundle = Streamlines([base + np.array([0, -i, 0]) for i in range(10)])
```

### Step 9: Assign orig_bundle = Streamlines(...)

```python
orig_bundle = Streamlines([base + np.array([0, i, 0]) for i in range(10)])
```

### Step 10: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 11: Assign profile = buan_profile(...)

```python
profile = buan_profile(model_bundle, bundle, orig_bundle, data, affine, no_disks=10)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(profile.shape, (10,))
```

### Step 13: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(profile, np.ones(10))
```

### Step 14: Assign profile = buan_profile(...)

```python
profile = buan_profile(model_bundle, bundle, orig_bundle, data, affine, no_disks=5)
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(profile.shape, (5,))
```

### Step 16: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(profile, np.ones(5))
```

### Step 17: Assign data_nan = value

```python
data_nan = np.ones((40, 40, 40), dtype=float) * np.nan
```

### Step 18: Assign profile = buan_profile(...)

```python
profile = buan_profile(model_bundle, bundle, orig_bundle, data_nan, affine, no_disks=10)
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(profile.shape, (10,))
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(np.all(np.isnan(profile)), True)
```

### Step 21: Assign empty_bundle = Streamlines(...)

```python
empty_bundle = Streamlines([])
```

### Step 22: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, buan_profile, model_bundle, empty_bundle, empty_bundle, data, affine, no_disks=10)
```


## Complete Example

```python
# Workflow
data = np.ones((40, 40, 40), dtype=float)
n_pts = 20
x = np.linspace(5, 34, n_pts)
y0 = 20.0
z0 = 20.0
base = np.vstack([x, np.ones(n_pts) * y0, np.ones(n_pts) * z0]).T
bundle = Streamlines([base + np.array([0, i, 0]) for i in range(10)])
model_bundle = Streamlines([base + np.array([0, -i, 0]) for i in range(10)])
orig_bundle = Streamlines([base + np.array([0, i, 0]) for i in range(10)])
affine = np.eye(4)
profile = buan_profile(model_bundle, bundle, orig_bundle, data, affine, no_disks=10)
npt.assert_equal(profile.shape, (10,))
npt.assert_almost_equal(profile, np.ones(10))
profile = buan_profile(model_bundle, bundle, orig_bundle, data, affine, no_disks=5)
npt.assert_equal(profile.shape, (5,))
npt.assert_almost_equal(profile, np.ones(5))
data_nan = np.ones((40, 40, 40), dtype=float) * np.nan
profile = buan_profile(model_bundle, bundle, orig_bundle, data_nan, affine, no_disks=10)
npt.assert_equal(profile.shape, (10,))
npt.assert_equal(np.all(np.isnan(profile)), True)
empty_bundle = Streamlines([])
npt.assert_raises(ValueError, buan_profile, model_bundle, empty_bundle, empty_bundle, data, affine, no_disks=10)
```

## Next Steps


---

*Source: test_analysis.py:140 | Complexity: Advanced | Last updated: 2026-05-18*