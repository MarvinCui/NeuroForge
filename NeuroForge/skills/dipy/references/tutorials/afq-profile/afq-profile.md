# How To: Afq Profile

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test afq profile

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.stats.analysis`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign data = np.ones(...)

```python
data = np.ones((10, 10, 10))
```

### Step 2: Assign bundle = Streamlines(...)

```python
bundle = Streamlines()
```

### Step 3: Call bundle.extend()

```python
bundle.extend(np.array([[[0, 0.0, 0], [1, 0.0, 0.0], [2, 0.0, 0.0]]]))
```

### Step 4: Call bundle.extend()

```python
bundle.extend(np.array([[[0, 0.0, 0.0], [1, 0.0, 0], [2, 0, 0.0]]]))
```

### Step 5: Assign profile = afq_profile(...)

```python
profile = afq_profile(data, bundle, np.eye(4))
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(profile, np.ones(100))
```

### Step 7: Assign profile = afq_profile(...)

```python
profile = afq_profile(data, bundle, np.eye(4), n_points=10, weights=None)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(profile, np.ones(10))
```

### Step 9: Assign profile = afq_profile(...)

```python
profile = afq_profile(data, bundle, np.eye(4), weights=gaussian_weights, stat=np.median)
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(profile, np.ones(100))
```

### Step 11: Assign profile = afq_profile(...)

```python
profile = afq_profile(data, bundle, np.eye(4), orient_by=bundle[0], weights=gaussian_weights, stat=np.median)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(profile, np.ones(100))
```

### Step 13: Assign profile = afq_profile(...)

```python
profile = afq_profile(data, bundle, np.eye(4), n_points=10, weights=None)
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(profile, np.ones(10))
```

### Step 15: Assign profile = afq_profile(...)

```python
profile = afq_profile(data, bundle, np.eye(4), n_points=10, weights=np.ones((2, 10)) * 0.5)
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(profile, np.ones(10))
```

### Step 17: Assign profile = afq_profile(...)

```python
profile = afq_profile(data, bundle, np.eye(4), n_points=10, stat=np.median)
```

### Step 18: Call npt.assert_equal()

```python
npt.assert_equal(profile, np.ones(10))
```

### Step 19: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, afq_profile, data, bundle, np.eye(4), n_points=10, weights=np.ones((2, 10)) * 0.6)
```

### Step 20: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 21: Assign unknown = value

```python
affine[:, 3] = [-1, 100, -20, 1]
```

### Step 22: Assign bundle._data = value

```python
bundle._data = bundle._data + affine[:3, 3]
```

### Step 23: Assign profile = afq_profile(...)

```python
profile = afq_profile(data, bundle, affine, n_points=10, weights=None)
```

### Step 24: Call npt.assert_equal()

```python
npt.assert_equal(profile, np.ones(10))
```

### Step 25: Assign empty_bundle = Streamlines(...)

```python
empty_bundle = Streamlines([])
```

### Step 26: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, afq_profile, data, empty_bundle, np.eye(4))
```


## Complete Example

```python
# Workflow
data = np.ones((10, 10, 10))
bundle = Streamlines()
bundle.extend(np.array([[[0, 0.0, 0], [1, 0.0, 0.0], [2, 0.0, 0.0]]]))
bundle.extend(np.array([[[0, 0.0, 0.0], [1, 0.0, 0], [2, 0, 0.0]]]))
profile = afq_profile(data, bundle, np.eye(4))
npt.assert_equal(profile, np.ones(100))
profile = afq_profile(data, bundle, np.eye(4), n_points=10, weights=None)
npt.assert_equal(profile, np.ones(10))
profile = afq_profile(data, bundle, np.eye(4), weights=gaussian_weights, stat=np.median)
npt.assert_equal(profile, np.ones(100))
profile = afq_profile(data, bundle, np.eye(4), orient_by=bundle[0], weights=gaussian_weights, stat=np.median)
npt.assert_equal(profile, np.ones(100))
profile = afq_profile(data, bundle, np.eye(4), n_points=10, weights=None)
npt.assert_equal(profile, np.ones(10))
profile = afq_profile(data, bundle, np.eye(4), n_points=10, weights=np.ones((2, 10)) * 0.5)
npt.assert_equal(profile, np.ones(10))
profile = afq_profile(data, bundle, np.eye(4), n_points=10, stat=np.median)
npt.assert_equal(profile, np.ones(10))
npt.assert_raises(ValueError, afq_profile, data, bundle, np.eye(4), n_points=10, weights=np.ones((2, 10)) * 0.6)
affine = np.eye(4)
affine[:, 3] = [-1, 100, -20, 1]
bundle._data = bundle._data + affine[:3, 3]
profile = afq_profile(data, bundle, affine, n_points=10, weights=None)
npt.assert_equal(profile, np.ones(10))
empty_bundle = Streamlines([])
npt.assert_raises(ValueError, afq_profile, data, empty_bundle, np.eye(4))
```

## Next Steps


---

*Source: test_analysis.py:75 | Complexity: Advanced | Last updated: 2026-05-18*