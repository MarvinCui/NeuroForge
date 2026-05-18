# How To: Calculate Tr

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the TR calculation.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.hemodynamic_models`


## Step-by-Step Guide

### Step 1: 'Test the TR calculation.'

```python
'Test the TR calculation.'
```

**Verification:**
```python
assert_almost_equal(estimated_tr, true_tr, 2)
```

### Step 2: Assign true_tr = 0.75

```python
true_tr = 0.75
```

### Step 3: Assign n_vols = 4

```python
n_vols = 4
```

### Step 4: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(true_tr / 2, n_vols * true_tr + true_tr / 2, n_vols + 1)
```

### Step 5: Assign estimated_tr = _calculate_tr(...)

```python
estimated_tr = _calculate_tr(frame_times)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(estimated_tr, true_tr, 2)
```


## Complete Example

```python
# Workflow
'Test the TR calculation.'
true_tr = 0.75
n_vols = 4
frame_times = np.linspace(true_tr / 2, n_vols * true_tr + true_tr / 2, n_vols + 1)
estimated_tr = _calculate_tr(frame_times)
assert_almost_equal(estimated_tr, true_tr, 2)
```

## Next Steps


---

*Source: test_hemodynamic_models.py:414 | Complexity: Intermediate | Last updated: 2026-05-18*