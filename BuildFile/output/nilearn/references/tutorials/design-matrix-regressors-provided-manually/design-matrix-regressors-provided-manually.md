# How To: Design Matrix Regressors Provided Manually

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test design matrix regressors provided manually

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn.glm.first_level.design_matrix`
- `_testing`

**Setup Required:**
```python
# Fixtures: rng, frame_times
```

## Step-by-Step Guide

### Step 1: Assign ax = rng.standard_normal(...)

```python
ax = rng.standard_normal(size=(len(frame_times), 4))
```

**Verification:**
```python
assert_almost_equal(X[:, 0], ax[:, 0])
```

### Step 2: Assign unknown = check_design_matrix(...)

```python
_, X, names = check_design_matrix(make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3, add_regs=ax))
```

**Verification:**
```python
assert len(names) == 8
```

### Step 3: Call assert_almost_equal()

```python
assert_almost_equal(X[:, 0], ax[:, 0])
```

**Verification:**
```python
assert X.shape[1] == 8
```

### Step 4: Assign axdf = pd.DataFrame(...)

```python
axdf = pd.DataFrame(ax)
```

**Verification:**
```python
assert_almost_equal(X1[:, 0], ax[:, 0])
```

### Step 5: Assign unknown = check_design_matrix(...)

```python
_, X1, names = check_design_matrix(make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3, add_regs=axdf))
```

**Verification:**
```python
assert_array_equal(names[:4], np.arange(4))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(X1[:, 0], ax[:, 0])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(names[:4], np.arange(4))
```


## Complete Example

```python
# Setup
# Fixtures: rng, frame_times

# Workflow
ax = rng.standard_normal(size=(len(frame_times), 4))
_, X, names = check_design_matrix(make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3, add_regs=ax))
assert_almost_equal(X[:, 0], ax[:, 0])
assert len(names) == 8
assert X.shape[1] == 8
axdf = pd.DataFrame(ax)
_, X1, names = check_design_matrix(make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3, add_regs=axdf))
assert_almost_equal(X1[:, 0], ax[:, 0])
assert_array_equal(names[:4], np.arange(4))
```

## Next Steps


---

*Source: test_design_matrix.py:98 | Complexity: Intermediate | Last updated: 2026-05-18*