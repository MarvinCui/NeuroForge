# How To: Vol Matching

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test vol matching

## Prerequisites

**Required Modules:**
- `os.path`
- `gzip`
- `numpy`
- `nose.tools`
- `numpy.testing`
- `dicom`


## Step-by-Step Guide

### Step 1: Assign dw_siemens = didw.wrapper_from_data(...)

```python
dw_siemens = didw.wrapper_from_data(DATA)
```

**Verification:**
```python
assert_true(dw_siemens.is_mosaic)
```

### Step 2: Call assert_true()

```python
assert_true(dw_siemens.is_mosaic)
```

**Verification:**
```python
assert_true(dw_siemens.is_csa)
```

### Step 3: Call assert_true()

```python
assert_true(dw_siemens.is_csa)
```

**Verification:**
```python
assert_true(dw_siemens.is_same_series(dw_siemens))
```

### Step 4: Call assert_true()

```python
assert_true(dw_siemens.is_same_series(dw_siemens))
```

**Verification:**
```python
assert_false(dw_plain.is_mosaic)
```

### Step 5: Assign dw_plain = didw.Wrapper(...)

```python
dw_plain = didw.Wrapper(DATA)
```

**Verification:**
```python
assert_false(dw_plain.is_csa)
```

### Step 6: Call assert_false()

```python
assert_false(dw_plain.is_mosaic)
```

**Verification:**
```python
assert_true(dw_plain.is_same_series(dw_plain))
```

### Step 7: Call assert_false()

```python
assert_false(dw_plain.is_csa)
```

**Verification:**
```python
assert_false(dw_plain.is_same_series(dw_siemens))
```

### Step 8: Call assert_true()

```python
assert_true(dw_plain.is_same_series(dw_plain))
```

**Verification:**
```python
assert_false(dw_siemens.is_same_series(dw_plain))
```

### Step 9: Call assert_false()

```python
assert_false(dw_plain.is_same_series(dw_siemens))
```

**Verification:**
```python
assert_true(dw_empty.is_same_series(dw_empty))
```

### Step 10: Call assert_false()

```python
assert_false(dw_siemens.is_same_series(dw_plain))
```

**Verification:**
```python
assert_false(dw_empty.is_same_series(dw_plain))
```

### Step 11: Assign dw_empty = didw.Wrapper(...)

```python
dw_empty = didw.Wrapper()
```

**Verification:**
```python
assert_false(dw_plain.is_same_series(dw_empty))
```

### Step 12: Call assert_true()

```python
assert_true(dw_empty.is_same_series(dw_empty))
```

**Verification:**
```python
assert_true(dw_empty.is_same_series(C()))
```

### Step 13: Call assert_false()

```python
assert_false(dw_empty.is_same_series(dw_plain))
```

### Step 14: Call assert_false()

```python
assert_false(dw_plain.is_same_series(dw_empty))
```

### Step 15: Call assert_true()

```python
assert_true(dw_empty.is_same_series(C()))
```

### Step 16: Assign series_signature = value

```python
series_signature = {}
```


## Complete Example

```python
# Workflow
dw_siemens = didw.wrapper_from_data(DATA)
assert_true(dw_siemens.is_mosaic)
assert_true(dw_siemens.is_csa)
assert_true(dw_siemens.is_same_series(dw_siemens))
dw_plain = didw.Wrapper(DATA)
assert_false(dw_plain.is_mosaic)
assert_false(dw_plain.is_csa)
assert_true(dw_plain.is_same_series(dw_plain))
assert_false(dw_plain.is_same_series(dw_siemens))
assert_false(dw_siemens.is_same_series(dw_plain))
dw_empty = didw.Wrapper()
assert_true(dw_empty.is_same_series(dw_empty))
assert_false(dw_empty.is_same_series(dw_plain))
assert_false(dw_plain.is_same_series(dw_empty))

class C(object):
    series_signature = {}
assert_true(dw_empty.is_same_series(C()))
```

## Next Steps


---

*Source: test_dicomwrappers.py:108 | Complexity: Advanced | Last updated: 2026-05-18*