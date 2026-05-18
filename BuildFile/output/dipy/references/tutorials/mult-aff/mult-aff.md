# How To: Mult Aff

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test matrix multiplication using None as identity

## Prerequisites

**Required Modules:**
- `nibabel.eulerangles`
- `numpy`
- `numpy.testing`
- `dipy.align`
- `dipy.align.imwarp`
- `dipy.core.interpolation`
- `dipy.data`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: 'Test matrix multiplication using None as identity'

```python
'Test matrix multiplication using None as identity'
```

**Verification:**
```python
assert_array_almost_equal(C, expected_mult)
```

### Step 2: Assign A = np.array(...)

```python
A = np.array([[1.0, 2.0], [3.0, 4.0]])
```

**Verification:**
```python
assert_array_almost_equal(C, A)
```

### Step 3: Assign B = np.array(...)

```python
B = np.array([[2.0, 0.0], [0.0, 2.0]])
```

**Verification:**
```python
assert_array_almost_equal(C, B)
```

### Step 4: Assign C = imwarp.mult_aff(...)

```python
C = imwarp.mult_aff(A, B)
```

**Verification:**
```python
assert_equal(C, None)
```

### Step 5: Assign expected_mult = np.array(...)

```python
expected_mult = np.array([[2.0, 4.0], [6.0, 8.0]])
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(C, expected_mult)
```

### Step 7: Assign C = imwarp.mult_aff(...)

```python
C = imwarp.mult_aff(A, None)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(C, A)
```

### Step 9: Assign C = imwarp.mult_aff(...)

```python
C = imwarp.mult_aff(None, B)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(C, B)
```

### Step 11: Assign C = imwarp.mult_aff(...)

```python
C = imwarp.mult_aff(None, None)
```

### Step 12: Call assert_equal()

```python
assert_equal(C, None)
```


## Complete Example

```python
# Workflow
'Test matrix multiplication using None as identity'
A = np.array([[1.0, 2.0], [3.0, 4.0]])
B = np.array([[2.0, 0.0], [0.0, 2.0]])
C = imwarp.mult_aff(A, B)
expected_mult = np.array([[2.0, 4.0], [6.0, 8.0]])
assert_array_almost_equal(C, expected_mult)
C = imwarp.mult_aff(A, None)
assert_array_almost_equal(C, A)
C = imwarp.mult_aff(None, B)
assert_array_almost_equal(C, B)
C = imwarp.mult_aff(None, None)
assert_equal(C, None)
```

## Next Steps


---

*Source: test_imwarp.py:24 | Complexity: Advanced | Last updated: 2026-05-18*