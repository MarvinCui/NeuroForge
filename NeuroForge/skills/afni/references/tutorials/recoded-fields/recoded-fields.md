# How To: Recoded Fields

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test recoded fields

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `py3k`
- `numpy`
- `casting`
- `tmpdirs`
- `spatialimages`
- `affines`
- `nifti1`
- `test_arraywriters`
- `numpy.testing`
- `nose.tools`
- `nose`
- `testing`


## Step-by-Step Guide

### Step 1: Assign hdr = Nifti1Header(...)

```python
hdr = Nifti1Header()
```

**Verification:**
```python
assert_equal(hdr.get_value_label('qform_code'), 'unknown')
```

### Step 2: Call assert_equal()

```python
assert_equal(hdr.get_value_label('qform_code'), 'unknown')
```

**Verification:**
```python
assert_equal(hdr.get_value_label('qform_code'), 'talairach')
```

### Step 3: Assign unknown = 3

```python
hdr['qform_code'] = 3
```

**Verification:**
```python
assert_equal(hdr.get_value_label('sform_code'), 'unknown')
```

### Step 4: Call assert_equal()

```python
assert_equal(hdr.get_value_label('qform_code'), 'talairach')
```

**Verification:**
```python
assert_equal(hdr.get_value_label('sform_code'), 'talairach')
```

### Step 5: Call assert_equal()

```python
assert_equal(hdr.get_value_label('sform_code'), 'unknown')
```

**Verification:**
```python
assert_equal(hdr.get_value_label('intent_code'), 'none')
```

### Step 6: Assign unknown = 3

```python
hdr['sform_code'] = 3
```

**Verification:**
```python
assert_equal(hdr.get_value_label('intent_code'), 't test')
```

### Step 7: Call assert_equal()

```python
assert_equal(hdr.get_value_label('sform_code'), 'talairach')
```

**Verification:**
```python
assert_equal(hdr.get_value_label('slice_code'), 'unknown')
```

### Step 8: Call assert_equal()

```python
assert_equal(hdr.get_value_label('intent_code'), 'none')
```

**Verification:**
```python
assert_equal(hdr.get_value_label('slice_code'), 'alternating decreasing')
```

### Step 9: Call hdr.set_intent()

```python
hdr.set_intent('t test', (10,), name='some score')
```

### Step 10: Call assert_equal()

```python
assert_equal(hdr.get_value_label('intent_code'), 't test')
```

### Step 11: Call assert_equal()

```python
assert_equal(hdr.get_value_label('slice_code'), 'unknown')
```

### Step 12: Assign unknown = 4

```python
hdr['slice_code'] = 4
```

### Step 13: Call assert_equal()

```python
assert_equal(hdr.get_value_label('slice_code'), 'alternating decreasing')
```


## Complete Example

```python
# Workflow
hdr = Nifti1Header()
assert_equal(hdr.get_value_label('qform_code'), 'unknown')
hdr['qform_code'] = 3
assert_equal(hdr.get_value_label('qform_code'), 'talairach')
assert_equal(hdr.get_value_label('sform_code'), 'unknown')
hdr['sform_code'] = 3
assert_equal(hdr.get_value_label('sform_code'), 'talairach')
assert_equal(hdr.get_value_label('intent_code'), 'none')
hdr.set_intent('t test', (10,), name='some score')
assert_equal(hdr.get_value_label('intent_code'), 't test')
assert_equal(hdr.get_value_label('slice_code'), 'unknown')
hdr['slice_code'] = 4
assert_equal(hdr.get_value_label('slice_code'), 'alternating decreasing')
```

## Next Steps


---

*Source: test_nifti1.py:859 | Complexity: Advanced | Last updated: 2026-05-18*