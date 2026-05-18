# How To: Unpack Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test unpack data

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.direction.peaks`
- `dipy.testing.decorators`
- `dipy.viz.horizon.util`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign pam_data = rng.random(...)

```python
pam_data = rng.random((10, 10))
```

### Step 2: Assign result = unpack_data(...)

```python
result = unpack_data(pam_data, return_size=2)
```

### Step 3: Call npt.assert_equal()

```python
npt.assert_equal(len(result), 2)
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(result[0], pam_data)
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(result[1], None)
```

### Step 6: Assign pam_tuple_1 = value

```python
pam_tuple_1 = (pam_data,)
```

### Step 7: Assign result = unpack_data(...)

```python
result = unpack_data(pam_tuple_1, return_size=3)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(len(result), 3)
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(result[0], pam_data)
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(result[1], None)
```

### Step 11: Call npt.assert_equal()

```python
npt.assert_equal(result[2], None)
```

### Step 12: Assign filename = 'test_file.pam'

```python
filename = 'test_file.pam'
```

### Step 13: Assign pam_tuple_2 = value

```python
pam_tuple_2 = (pam_data, filename)
```

### Step 14: Assign result = unpack_data(...)

```python
result = unpack_data(pam_tuple_2, return_size=2)
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(len(result), 2)
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(result[0], pam_data)
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(result[1], filename)
```

### Step 18: Assign pam_tuple_3 = value

```python
pam_tuple_3 = (pam_data, filename, 'extra_item')
```

### Step 19: Assign result = unpack_data(...)

```python
result = unpack_data(pam_tuple_3, return_size=3)
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(result, pam_tuple_3)
```

### Step 21: Call npt.assert_equal()

```python
npt.assert_equal(len(result), 3)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
pam_data = rng.random((10, 10))
result = unpack_data(pam_data, return_size=2)
npt.assert_equal(len(result), 2)
npt.assert_equal(result[0], pam_data)
npt.assert_equal(result[1], None)
pam_tuple_1 = (pam_data,)
result = unpack_data(pam_tuple_1, return_size=3)
npt.assert_equal(len(result), 3)
npt.assert_equal(result[0], pam_data)
npt.assert_equal(result[1], None)
npt.assert_equal(result[2], None)
filename = 'test_file.pam'
pam_tuple_2 = (pam_data, filename)
result = unpack_data(pam_tuple_2, return_size=2)
npt.assert_equal(len(result), 2)
npt.assert_equal(result[0], pam_data)
npt.assert_equal(result[1], filename)
pam_tuple_3 = (pam_data, filename, 'extra_item')
result = unpack_data(pam_tuple_3, return_size=3)
npt.assert_equal(result, pam_tuple_3)
npt.assert_equal(len(result), 3)
```

## Next Steps


---

*Source: test_util.py:178 | Complexity: Advanced | Last updated: 2026-05-18*