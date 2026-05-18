# How To: As Native

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test as native

## Prerequisites

**Required Modules:**
- `sys`
- `numpy`
- `numpy.testing`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.arrfuncs`


## Step-by-Step Guide

### Step 1: Assign arr = np.arange(...)

```python
arr = np.arange(5)
```

**Verification:**
```python
assert_equal(arr.dtype.byteorder, '=')
```

### Step 2: Call assert_equal()

```python
assert_equal(arr.dtype.byteorder, '=')
```

**Verification:**
```python
assert_true(arr is narr)
```

### Step 3: Assign narr = as_native_array(...)

```python
narr = as_native_array(arr)
```

**Verification:**
```python
assert_equal(barr.dtype.byteorder, SWAPPED_ORDER)
```

### Step 4: Call assert_true()

```python
assert_true(arr is narr)
```

**Verification:**
```python
assert_false(barr is narr)
```

### Step 5: Assign sdt = arr.view(...)

```python
sdt = arr.view(arr.dtype.newbyteorder('s'))
```

**Verification:**
```python
assert_array_equal(barr, narr)
```

### Step 6: Assign barr = arr.astype(...)

```python
barr = arr.astype(sdt.dtype)
```

**Verification:**
```python
assert_equal(narr.dtype.byteorder, NATIVE_ORDER)
```

### Step 7: Call assert_equal()

```python
assert_equal(barr.dtype.byteorder, SWAPPED_ORDER)
```

### Step 8: Assign narr = as_native_array(...)

```python
narr = as_native_array(barr)
```

### Step 9: Call assert_false()

```python
assert_false(barr is narr)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(barr, narr)
```

### Step 11: Call assert_equal()

```python
assert_equal(narr.dtype.byteorder, NATIVE_ORDER)
```


## Complete Example

```python
# Workflow
arr = np.arange(5)
assert_equal(arr.dtype.byteorder, '=')
narr = as_native_array(arr)
assert_true(arr is narr)
sdt = arr.view(arr.dtype.newbyteorder('s'))
barr = arr.astype(sdt.dtype)
assert_equal(barr.dtype.byteorder, SWAPPED_ORDER)
narr = as_native_array(barr)
assert_false(barr is narr)
assert_array_equal(barr, narr)
assert_equal(narr.dtype.byteorder, NATIVE_ORDER)
```

## Next Steps


---

*Source: test_arrfuncs.py:16 | Complexity: Advanced | Last updated: 2026-05-18*