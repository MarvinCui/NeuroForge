# How To: Contrast Padding

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test contrast padding

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
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
n, p, q = (100, 80, 10)
```

### Step 2: Assign unknown = value

```python
X, Y = (rng.standard_normal(size=(p, q)), rng.standard_normal(size=(p, n)))
```

### Step 3: Assign unknown = run_glm(...)

```python
labels, results = run_glm(Y, X, 'ar1')
```

### Step 4: Assign con_val = value

```python
con_val = [1, 1]
```

### Step 5: Assign con_val = value

```python
con_val = np.eye(q)[:3, :3]
```

### Step 6: Call compute_contrast.z_score()

```python
compute_contrast(labels, results, con_val, stat_type='F').z_score()
```

### Step 7: Call compute_contrast.z_score()

```python
compute_contrast(labels, results, con_val).z_score()
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n, p, q = (100, 80, 10)
X, Y = (rng.standard_normal(size=(p, q)), rng.standard_normal(size=(p, n)))
labels, results = run_glm(Y, X, 'ar1')
con_val = [1, 1]
with pytest.warns(UserWarning, match='The rest of the contrast was padded with zeros.'):
    compute_contrast(labels, results, con_val).z_score()
con_val = np.eye(q)[:3, :3]
compute_contrast(labels, results, con_val, stat_type='F').z_score()
```

## Next Steps


---

*Source: test_contrasts.py:279 | Complexity: Intermediate | Last updated: 2026-05-18*