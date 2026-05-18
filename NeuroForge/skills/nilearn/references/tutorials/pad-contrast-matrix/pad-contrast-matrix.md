# How To: Pad Contrast Matrix

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test for contrasts padding before plotting.

See https://github.com/nilearn/nilearn/issues/4211

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.design_matrix`
- `nilearn.plotting.matrix._utils`


## Step-by-Step Guide

### Step 1: 'Test for contrasts padding before plotting.\n\n    See https://github.com/nilearn/nilearn/issues/4211\n    '

```python
'Test for contrasts padding before plotting.\n\n    See https://github.com/nilearn/nilearn/issues/4211\n    '
```

**Verification:**
```python
assert_array_equal(padded_contrast, np.array([[1, -1, 0, 0]]))
```

### Step 2: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 127 * 1.0, 128)
```

**Verification:**
```python
assert_array_equal(padded_contrast, np.array([[1, 0, 0, 0], [0, 1, 0, 0], [0, 0, 1, 0]]))
```

### Step 3: Assign dmtx = make_first_level_design_matrix(...)

```python
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
```

### Step 4: Assign contrast = np.array(...)

```python
contrast = np.array([[1, -1]])
```

### Step 5: Assign padded_contrast = pad_contrast_matrix(...)

```python
padded_contrast = pad_contrast_matrix(contrast, dmtx)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(padded_contrast, np.array([[1, -1, 0, 0]]))
```

### Step 7: Assign contrast = np.eye(...)

```python
contrast = np.eye(3)
```

### Step 8: Assign padded_contrast = pad_contrast_matrix(...)

```python
padded_contrast = pad_contrast_matrix(contrast, dmtx)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(padded_contrast, np.array([[1, 0, 0, 0], [0, 1, 0, 0], [0, 0, 1, 0]]))
```


## Complete Example

```python
# Workflow
'Test for contrasts padding before plotting.\n\n    See https://github.com/nilearn/nilearn/issues/4211\n    '
frame_times = np.linspace(0, 127 * 1.0, 128)
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
contrast = np.array([[1, -1]])
padded_contrast = pad_contrast_matrix(contrast, dmtx)
assert_array_equal(padded_contrast, np.array([[1, -1, 0, 0]]))
contrast = np.eye(3)
padded_contrast = pad_contrast_matrix(contrast, dmtx)
assert_array_equal(padded_contrast, np.array([[1, 0, 0, 0], [0, 1, 0, 0], [0, 0, 1, 0]]))
```

## Next Steps


---

*Source: test_utils.py:20 | Complexity: Advanced | Last updated: 2026-05-18*