# How To: Getbyintent

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test getbyintent

## Prerequisites

**Required Modules:**
- `__future__`
- `os.path`
- `numpy`
- `nifti1`
- `tmpdirs`
- `numpy.testing`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign img = gi.read(...)

```python
img = gi.read(DATA_FILE1)
```

**Verification:**
```python
assert_equal(len(da), 1)
```

### Step 2: Assign da = img.getArraysFromIntent(...)

```python
da = img.getArraysFromIntent('NIFTI_INTENT_POINTSET')
```

**Verification:**
```python
assert_equal(len(da), 1)
```

### Step 3: Call assert_equal()

```python
assert_equal(len(da), 1)
```

**Verification:**
```python
assert_equal(len(da), 0)
```

### Step 4: Assign da = img.getArraysFromIntent(...)

```python
da = img.getArraysFromIntent('NIFTI_INTENT_TRIANGLE')
```

**Verification:**
```python
assert_equal(da, [])
```

### Step 5: Call assert_equal()

```python
assert_equal(len(da), 1)
```

### Step 6: Assign da = img.getArraysFromIntent(...)

```python
da = img.getArraysFromIntent('NIFTI_INTENT_CORREL')
```

### Step 7: Call assert_equal()

```python
assert_equal(len(da), 0)
```

### Step 8: Call assert_equal()

```python
assert_equal(da, [])
```


## Complete Example

```python
# Workflow
img = gi.read(DATA_FILE1)
da = img.getArraysFromIntent('NIFTI_INTENT_POINTSET')
assert_equal(len(da), 1)
da = img.getArraysFromIntent('NIFTI_INTENT_TRIANGLE')
assert_equal(len(da), 1)
da = img.getArraysFromIntent('NIFTI_INTENT_CORREL')
assert_equal(len(da), 0)
assert_equal(da, [])
```

## Next Steps


---

*Source: test_giftiio.py:174 | Complexity: Advanced | Last updated: 2026-05-18*