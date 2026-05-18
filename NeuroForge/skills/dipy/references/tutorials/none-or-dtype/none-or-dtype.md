# How To: None Or Dtype

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test none or dtype

## Prerequisites

**Required Modules:**
- `pathlib`
- `sys`
- `tempfile`
- `numpy.testing`
- `dipy.workflows.base`
- `dipy.workflows.flow_runner`
- `dipy.workflows.tests.workflow_tests_utils`


## Step-by-Step Guide

### Step 1: Assign dec = none_or_dtype(...)

```python
dec = none_or_dtype(int)
```

### Step 2: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, dec, 'my value')
```

### Step 3: Call npt.assert_equal()

```python
npt.assert_equal(dec(4), 4)
```

### Step 4: Assign dec = none_or_dtype(...)

```python
dec = none_or_dtype(str)
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(dec(4), '4')
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(dec('my value'), 'my value')
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(dec([4]), '[4]')
```

### Step 8: Assign dec = none_or_dtype(...)

```python
dec = none_or_dtype(float)
```

### Step 9: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, dec, 'my value')
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(dec(True), 1.0)
```

### Step 11: Call npt.assert_equal()

```python
npt.assert_equal(dec(4), 4.0)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(dec(4.0), 4.0)
```

### Step 13: Assign dec = none_or_dtype(...)

```python
dec = none_or_dtype(bool)
```

### Step 14: Assign dec = none_or_dtype(...)

```python
dec = none_or_dtype(tuple)
```

### Step 15: Assign dec = none_or_dtype(...)

```python
dec = none_or_dtype(typ)
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(dec('None'), 'None')
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(dec('none'), 'None')
```

### Step 18: Call npt.assert_raises()

```python
npt.assert_raises(TypeError, dec, val)
```


## Complete Example

```python
# Workflow
for typ in [int, float, str, tuple, list]:
    dec = none_or_dtype(typ)
    npt.assert_equal(dec('None'), 'None')
    npt.assert_equal(dec('none'), 'None')
dec = none_or_dtype(int)
npt.assert_raises(ValueError, dec, 'my value')
npt.assert_equal(dec(4), 4)
dec = none_or_dtype(str)
npt.assert_equal(dec(4), '4')
npt.assert_equal(dec('my value'), 'my value')
npt.assert_equal(dec([4]), '[4]')
dec = none_or_dtype(float)
npt.assert_raises(ValueError, dec, 'my value')
for val in [(4,), [4]]:
    npt.assert_raises(TypeError, dec, val)
npt.assert_equal(dec(True), 1.0)
npt.assert_equal(dec(4), 4.0)
npt.assert_equal(dec(4.0), 4.0)
dec = none_or_dtype(bool)
dec = none_or_dtype(tuple)
```

## Next Steps


---

*Source: test_iap.py:23 | Complexity: Advanced | Last updated: 2026-05-18*