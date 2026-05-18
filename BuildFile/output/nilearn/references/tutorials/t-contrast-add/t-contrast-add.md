# How To: T Contrast Add

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test t contrast add

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `sklearn.datasets`
- `sklearn.linear_model`
- `nilearn.glm.contrasts`
- `nilearn.glm.first_level`

**Setup Required:**
```python
# Fixtures: set_up_glm, rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = set_up_glm(...)

```python
labels, results, q = set_up_glm(rng, 'ols')
```

**Verification:**
```python
assert_almost_equal(z_vals.mean(), 0, 0)
```

### Step 2: Assign unknown = value

```python
c1, c2 = (np.eye(q)[0], np.eye(q)[1])
```

**Verification:**
```python
assert_almost_equal(z_vals.std(), 1, 0)
```

### Step 3: Assign con = value

```python
con = compute_contrast(labels, results, c1) + compute_contrast(labels, results, c2)
```

### Step 4: Assign z_vals = con.z_score(...)

```python
z_vals = con.z_score()
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(z_vals.mean(), 0, 0)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(z_vals.std(), 1, 0)
```


## Complete Example

```python
# Setup
# Fixtures: set_up_glm, rng

# Workflow
labels, results, q = set_up_glm(rng, 'ols')
c1, c2 = (np.eye(q)[0], np.eye(q)[1])
con = compute_contrast(labels, results, c1) + compute_contrast(labels, results, c2)
z_vals = con.z_score()
assert_almost_equal(z_vals.mean(), 0, 0)
assert_almost_equal(z_vals.std(), 1, 0)
```

## Next Steps


---

*Source: test_contrasts.py:85 | Complexity: Intermediate | Last updated: 2026-05-18*