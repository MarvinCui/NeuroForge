# How To: Inplace

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test inplace

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.denoise.gibbs`


## Step-by-Step Guide

### Step 1: Assign input_2d = image_gibbs.copy(...)

```python
input_2d = image_gibbs.copy()
```

**Verification:**
```python
assert_raises(AssertionError, assert_array_almost_equal, input_2d, output_2d)
```

### Step 2: Assign input_3d = np.stack(...)

```python
input_3d = np.stack([input_2d, input_2d], axis=2)
```

**Verification:**
```python
assert_array_almost_equal(input_2d, output_2d)
```

### Step 3: Assign input_4d = np.stack(...)

```python
input_4d = np.stack([input_3d, input_3d], axis=3)
```

**Verification:**
```python
assert_raises(AssertionError, assert_array_almost_equal, input_3d, output_3d)
```

### Step 4: Assign output_2d = gibbs_removal(...)

```python
output_2d = gibbs_removal(input_2d, inplace=False)
```

**Verification:**
```python
assert_array_almost_equal(input_3d, output_3d)
```

### Step 5: Call assert_raises()

```python
assert_raises(AssertionError, assert_array_almost_equal, input_2d, output_2d)
```

**Verification:**
```python
assert_raises(AssertionError, assert_array_almost_equal, input_4d, output_4d)
```

### Step 6: Assign output_2d = gibbs_removal(...)

```python
output_2d = gibbs_removal(input_2d, inplace=True)
```

**Verification:**
```python
assert_array_almost_equal(input_4d, output_4d)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(input_2d, output_2d)
```

### Step 8: Assign output_3d = gibbs_removal(...)

```python
output_3d = gibbs_removal(input_3d, inplace=False)
```

### Step 9: Call assert_raises()

```python
assert_raises(AssertionError, assert_array_almost_equal, input_3d, output_3d)
```

### Step 10: Assign output_3d = gibbs_removal(...)

```python
output_3d = gibbs_removal(input_3d, inplace=True)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(input_3d, output_3d)
```

### Step 12: Assign output_4d = gibbs_removal(...)

```python
output_4d = gibbs_removal(input_4d, inplace=False)
```

### Step 13: Call assert_raises()

```python
assert_raises(AssertionError, assert_array_almost_equal, input_4d, output_4d)
```

### Step 14: Assign output_4d = gibbs_removal(...)

```python
output_4d = gibbs_removal(input_4d, inplace=True)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(input_4d, output_4d)
```


## Complete Example

```python
# Workflow
input_2d = image_gibbs.copy()
input_3d = np.stack([input_2d, input_2d], axis=2)
input_4d = np.stack([input_3d, input_3d], axis=3)
output_2d = gibbs_removal(input_2d, inplace=False)
assert_raises(AssertionError, assert_array_almost_equal, input_2d, output_2d)
output_2d = gibbs_removal(input_2d, inplace=True)
assert_array_almost_equal(input_2d, output_2d)
output_3d = gibbs_removal(input_3d, inplace=False)
assert_raises(AssertionError, assert_array_almost_equal, input_3d, output_3d)
output_3d = gibbs_removal(input_3d, inplace=True)
assert_array_almost_equal(input_3d, output_3d)
output_4d = gibbs_removal(input_4d, inplace=False)
assert_raises(AssertionError, assert_array_almost_equal, input_4d, output_4d)
output_4d = gibbs_removal(input_4d, inplace=True)
assert_array_almost_equal(input_4d, output_4d)
```

## Next Steps


---

*Source: test_gibbs.py:69 | Complexity: Advanced | Last updated: 2026-05-18*