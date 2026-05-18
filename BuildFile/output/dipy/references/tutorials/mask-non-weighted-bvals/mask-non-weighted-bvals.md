# How To: Mask Non Weighted Bvals

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mask non weighted bvals

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign bvals = np.array(...)

```python
bvals = np.array([0.0, 100.0, 200.0, 300.0, 400.0])
```

**Verification:**
```python
assert np.array_equal(obtained_val, expected_val)
```

### Step 2: Assign b0_threshold = 0.0

```python
b0_threshold = 0.0
```

**Verification:**
```python
assert np.array_equal(obtained_val, expected_val)
```

### Step 3: Assign expected_val = np.asarray(...)

```python
expected_val = np.asarray([True, False, False, False, False])
```

**Verification:**
```python
assert np.array_equal(obtained_val, expected_val)
```

### Step 4: Assign obtained_val = mask_non_weighted_bvals(...)

```python
obtained_val = mask_non_weighted_bvals(bvals, b0_threshold)
```

**Verification:**
```python
assert np.array_equal(obtained_val, expected_val)
```

### Step 5: Assign b0_threshold = 50

```python
b0_threshold = 50
```

### Step 6: Assign obtained_val = mask_non_weighted_bvals(...)

```python
obtained_val = mask_non_weighted_bvals(bvals, b0_threshold)
```

**Verification:**
```python
assert np.array_equal(obtained_val, expected_val)
```

### Step 7: Assign b0_threshold = 200.0

```python
b0_threshold = 200.0
```

### Step 8: Assign expected_val = np.asarray(...)

```python
expected_val = np.asarray([True, True, True, False, False])
```

### Step 9: Assign obtained_val = mask_non_weighted_bvals(...)

```python
obtained_val = mask_non_weighted_bvals(bvals, b0_threshold)
```

**Verification:**
```python
assert np.array_equal(obtained_val, expected_val)
```


## Complete Example

```python
# Workflow
bvals = np.array([0.0, 100.0, 200.0, 300.0, 400.0])
b0_threshold = 0.0
expected_val = np.asarray([True, False, False, False, False])
obtained_val = mask_non_weighted_bvals(bvals, b0_threshold)
assert np.array_equal(obtained_val, expected_val)
b0_threshold = 50
obtained_val = mask_non_weighted_bvals(bvals, b0_threshold)
assert np.array_equal(obtained_val, expected_val)
b0_threshold = 200.0
expected_val = np.asarray([True, True, True, False, False])
obtained_val = mask_non_weighted_bvals(bvals, b0_threshold)
assert np.array_equal(obtained_val, expected_val)
```

## Next Steps


---

*Source: test_gradients.py:41 | Complexity: Advanced | Last updated: 2026-05-18*