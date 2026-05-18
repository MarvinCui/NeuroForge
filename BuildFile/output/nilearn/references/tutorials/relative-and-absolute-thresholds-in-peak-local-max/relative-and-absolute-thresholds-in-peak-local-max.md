# How To: Relative And Absolute Thresholds In Peak Local Max

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test relative and absolute thresholds in peak local max

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn._utils`
- `nilearn._utils.ndimage`


## Step-by-Step Guide

### Step 1: Assign image = np.zeros(...)

```python
image = np.zeros((5, 5))
```

### Step 2: Assign unknown = 10

```python
image[1, 1] = 10
```

### Step 3: Assign unknown = 20

```python
image[3, 3] = 20
```

### Step 4: Assign peaks_rel = peak_local_max(...)

```python
peaks_rel = peak_local_max(image, min_distance=1, threshold_rel=0.5)
```

### Step 5: Call np.testing.assert_equal()

```python
np.testing.assert_equal(len(peaks_rel[peaks_rel == 1]), 1)
```

### Step 6: Assign peaks_abs = peak_local_max(...)

```python
peaks_abs = peak_local_max(image, min_distance=1, threshold_abs=10)
```

### Step 7: Call np.testing.assert_equal()

```python
np.testing.assert_equal(len(peaks_abs[peaks_abs == 1]), 1)
```


## Complete Example

```python
# Workflow
image = np.zeros((5, 5))
image[1, 1] = 10
image[3, 3] = 20
peaks_rel = peak_local_max(image, min_distance=1, threshold_rel=0.5)
np.testing.assert_equal(len(peaks_rel[peaks_rel == 1]), 1)
peaks_abs = peak_local_max(image, min_distance=1, threshold_abs=10)
np.testing.assert_equal(len(peaks_abs[peaks_abs == 1]), 1)
```

## Next Steps


---

*Source: test_ndimage.py:50 | Complexity: Intermediate | Last updated: 2026-05-18*