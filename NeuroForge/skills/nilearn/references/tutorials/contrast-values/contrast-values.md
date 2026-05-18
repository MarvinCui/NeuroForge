# How To: Contrast Values

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test contrast values

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
labels, results, q = set_up_glm(rng, 'ar1', bins=1)
```

**Verification:**
```python
assert_almost_equal(np.ravel(con.stat()), t_ref)
```

### Step 2: Assign cval = value

```python
cval = np.eye(q)[0]
```

**Verification:**
```python
assert_almost_equal(np.ravel(con.stat()), F_ref, 3)
```

### Step 3: Assign con = compute_contrast(...)

```python
con = compute_contrast(labels, results, cval)
```

### Step 4: Assign t_ref = value

```python
t_ref = next(iter(results.values())).Tcontrast(cval).t
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(np.ravel(con.stat()), t_ref)
```

### Step 6: Assign cval = value

```python
cval = np.eye(q)[:3]
```

### Step 7: Assign con = compute_contrast(...)

```python
con = compute_contrast(labels, results, cval)
```

### Step 8: Assign F_ref = value

```python
F_ref = next(iter(results.values())).Fcontrast(cval).F
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(np.ravel(con.stat()), F_ref, 3)
```


## Complete Example

```python
# Setup
# Fixtures: set_up_glm, rng

# Workflow
labels, results, q = set_up_glm(rng, 'ar1', bins=1)
cval = np.eye(q)[0]
con = compute_contrast(labels, results, cval)
t_ref = next(iter(results.values())).Tcontrast(cval).t
assert_almost_equal(np.ravel(con.stat()), t_ref)
cval = np.eye(q)[:3]
con = compute_contrast(labels, results, cval)
F_ref = next(iter(results.values())).Fcontrast(cval).F
assert_almost_equal(np.ravel(con.stat()), F_ref, 3)
```

## Next Steps


---

*Source: test_contrasts.py:169 | Complexity: Advanced | Last updated: 2026-05-18*