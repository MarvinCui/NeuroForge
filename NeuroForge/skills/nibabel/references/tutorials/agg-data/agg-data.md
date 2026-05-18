# How To: Agg Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test agg data

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.tmpdirs`
- `fileholders`
- `nifti1`
- `testing`
- `test_parse_gifti_fast`
- `gifti`


## Step-by-Step Guide

### Step 1: Assign surf_gii_img = load(...)

```python
surf_gii_img = load(get_test_data('gifti', 'ascii.gii'))
```

**Verification:**
```python
assert surf_gii_img.agg_data() == (point_data, triangle_data)
```

### Step 2: Assign func_gii_img = load(...)

```python
func_gii_img = load(get_test_data('gifti', 'task.func.gii'))
```

**Verification:**
```python
assert_array_equal(func_gii_img.agg_data(), func_data)
```

### Step 3: Assign shape_gii_img = load(...)

```python
shape_gii_img = load(get_test_data('gifti', 'rh.shape.curv.gii'))
```

**Verification:**
```python
assert_array_equal(shape_gii_img.agg_data(), shape_data)
```

### Step 4: Assign point_data = value

```python
point_data = surf_gii_img.get_arrays_from_intent('pointset')[0].data
```

**Verification:**
```python
assert_array_equal(surf_gii_img.agg_data('pointset'), point_data)
```

### Step 5: Assign triangle_data = value

```python
triangle_data = surf_gii_img.get_arrays_from_intent('triangle')[0].data
```

**Verification:**
```python
assert_array_equal(surf_gii_img.agg_data('triangle'), triangle_data)
```

### Step 6: Assign func_da = func_gii_img.get_arrays_from_intent(...)

```python
func_da = func_gii_img.get_arrays_from_intent('time series')
```

**Verification:**
```python
assert_array_equal(func_gii_img.agg_data('time series'), func_data)
```

### Step 7: Assign func_data = np.column_stack(...)

```python
func_data = np.column_stack(tuple((da.data for da in func_da)))
```

**Verification:**
```python
assert_array_equal(shape_gii_img.agg_data('shape'), shape_data)
```

### Step 8: Assign shape_data = value

```python
shape_data = shape_gii_img.get_arrays_from_intent('shape')[0].data
```

**Verification:**
```python
assert surf_gii_img.agg_data('time series') == ()
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(func_gii_img.agg_data(), func_data)
```

**Verification:**
```python
assert func_gii_img.agg_data('triangle') == ()
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(shape_gii_img.agg_data(), shape_data)
```

**Verification:**
```python
assert shape_gii_img.agg_data('pointset') == ()
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(surf_gii_img.agg_data('pointset'), point_data)
```

**Verification:**
```python
assert surf_gii_img.agg_data(('pointset', 'triangle')) == (point_data, triangle_data)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(surf_gii_img.agg_data('triangle'), triangle_data)
```

**Verification:**
```python
assert surf_gii_img.agg_data(('triangle', 'pointset')) == (triangle_data, point_data)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(func_gii_img.agg_data('time series'), func_data)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(shape_gii_img.agg_data('shape'), shape_data)
```

**Verification:**
```python
assert surf_gii_img.agg_data('time series') == ()
```


## Complete Example

```python
# Workflow
surf_gii_img = load(get_test_data('gifti', 'ascii.gii'))
func_gii_img = load(get_test_data('gifti', 'task.func.gii'))
shape_gii_img = load(get_test_data('gifti', 'rh.shape.curv.gii'))
point_data = surf_gii_img.get_arrays_from_intent('pointset')[0].data
triangle_data = surf_gii_img.get_arrays_from_intent('triangle')[0].data
func_da = func_gii_img.get_arrays_from_intent('time series')
func_data = np.column_stack(tuple((da.data for da in func_da)))
shape_data = shape_gii_img.get_arrays_from_intent('shape')[0].data
assert surf_gii_img.agg_data() == (point_data, triangle_data)
assert_array_equal(func_gii_img.agg_data(), func_data)
assert_array_equal(shape_gii_img.agg_data(), shape_data)
assert_array_equal(surf_gii_img.agg_data('pointset'), point_data)
assert_array_equal(surf_gii_img.agg_data('triangle'), triangle_data)
assert_array_equal(func_gii_img.agg_data('time series'), func_data)
assert_array_equal(shape_gii_img.agg_data('shape'), shape_data)
assert surf_gii_img.agg_data('time series') == ()
assert func_gii_img.agg_data('triangle') == ()
assert shape_gii_img.agg_data('pointset') == ()
assert surf_gii_img.agg_data(('pointset', 'triangle')) == (point_data, triangle_data)
assert surf_gii_img.agg_data(('triangle', 'pointset')) == (triangle_data, point_data)
```

## Next Steps


---

*Source: test_gifti.py:38 | Complexity: Advanced | Last updated: 2026-05-18*