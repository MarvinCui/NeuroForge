# How To: Mean Distances

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mean distances

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.featurespeed`
- `dipy.segment.metric`
- `dipy.segment.metricspeed`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.core.geometry`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign nb_slines = 10

```python
nb_slines = 10
```

**Verification:**
```python
assert_almost_equal(mean_l2_dist, mean_norm)
```

### Step 2: Assign nb_pts = 22

```python
nb_pts = 22
```

**Verification:**
```python
assert_almost_equal(mean_l1_dist, mean_norm)
```

### Step 3: Assign dim = 3

```python
dim = 3
```

### Step 4: Assign a = rng.random(...)

```python
a = rng.random((nb_slines, nb_pts, dim))
```

### Step 5: Assign b = rng.random(...)

```python
b = rng.random((nb_slines, nb_pts, dim))
```

### Step 6: Assign diff = value

```python
diff = a - b
```

### Step 7: Assign mean_l2_dist = dipymetric.mean_euclidean_distance(...)

```python
mean_l2_dist = dipymetric.mean_euclidean_distance(a, b)
```

### Step 8: Assign diff_norm = np.linalg.norm(...)

```python
diff_norm = np.linalg.norm(diff.reshape((-1, dim)), ord=2, axis=-1)
```

### Step 9: Assign mean_norm = np.mean(...)

```python
mean_norm = np.mean(diff_norm.reshape((nb_slines, -1)), axis=-1)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(mean_l2_dist, mean_norm)
```

### Step 11: Assign mean_l1_dist = dipymetric.mean_manhattan_distance(...)

```python
mean_l1_dist = dipymetric.mean_manhattan_distance(a, b)
```

### Step 12: Assign diff_norm = np.linalg.norm(...)

```python
diff_norm = np.linalg.norm(diff.reshape((-1, dim)), ord=1, axis=-1)
```

### Step 13: Assign mean_norm = np.mean(...)

```python
mean_norm = np.mean(diff_norm.reshape((nb_slines, -1)), axis=-1)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(mean_l1_dist, mean_norm)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
nb_slines = 10
nb_pts = 22
dim = 3
a = rng.random((nb_slines, nb_pts, dim))
b = rng.random((nb_slines, nb_pts, dim))
diff = a - b
mean_l2_dist = dipymetric.mean_euclidean_distance(a, b)
diff_norm = np.linalg.norm(diff.reshape((-1, dim)), ord=2, axis=-1)
mean_norm = np.mean(diff_norm.reshape((nb_slines, -1)), axis=-1)
assert_almost_equal(mean_l2_dist, mean_norm)
mean_l1_dist = dipymetric.mean_manhattan_distance(a, b)
diff_norm = np.linalg.norm(diff.reshape((-1, dim)), ord=1, axis=-1)
mean_norm = np.mean(diff_norm.reshape((nb_slines, -1)), axis=-1)
assert_almost_equal(mean_l1_dist, mean_norm)
```

## Next Steps


---

*Source: test_metric.py:272 | Complexity: Advanced | Last updated: 2026-05-18*