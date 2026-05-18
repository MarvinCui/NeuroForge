# How To: F Contrast Add

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test f contrast add

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
labels, results, q = set_up_glm(rng, 'ar1')
```

**Verification:**
```python
assert_almost_equal(z_vals.mean(), 0, 0)
```

### Step 2: Assign unknown = value

```python
c1, c2 = (np.eye(q)[:2], np.eye(q)[2:4])
```

**Verification:**
```python
assert_almost_equal(z_vals.std(), 1, 0)
```

### Step 3: Assign con = value

```python
con = compute_contrast(labels, results, c1) + compute_contrast(labels, results, c2)
```

**Verification:**
```python
assert_almost_equal(con1.effect * 2, con2.effect)
```

### Step 4: Assign z_vals = con.z_score(...)

```python
z_vals = con.z_score()
```

**Verification:**
```python
assert_almost_equal(con1.variance * 2, con2.variance)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(z_vals.mean(), 0, 0)
```

**Verification:**
```python
assert_almost_equal(con1.stat() * 2, con2.stat())
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(z_vals.std(), 1, 0)
```

### Step 7: Assign con1 = compute_contrast(...)

```python
con1 = compute_contrast(labels, results, c1)
```

### Step 8: Assign con2 = value

```python
con2 = compute_contrast(labels, results, c1) + compute_contrast(labels, results, c1)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(con1.effect * 2, con2.effect)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(con1.variance * 2, con2.variance)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(con1.stat() * 2, con2.stat())
```


## Complete Example

```python
# Setup
# Fixtures: set_up_glm, rng

# Workflow
labels, results, q = set_up_glm(rng, 'ar1')
c1, c2 = (np.eye(q)[:2], np.eye(q)[2:4])
con = compute_contrast(labels, results, c1) + compute_contrast(labels, results, c2)
z_vals = con.z_score()
assert_almost_equal(z_vals.mean(), 0, 0)
assert_almost_equal(z_vals.std(), 1, 0)
con1 = compute_contrast(labels, results, c1)
con2 = compute_contrast(labels, results, c1) + compute_contrast(labels, results, c1)
assert_almost_equal(con1.effect * 2, con2.effect)
assert_almost_equal(con1.variance * 2, con2.variance)
assert_almost_equal(con1.stat() * 2, con2.stat())
```

## Next Steps


---

*Source: test_contrasts.py:136 | Complexity: Advanced | Last updated: 2026-05-18*