# How To: Slice Indicator

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test slice indicator

## Prerequisites

**Required Modules:**
- `os.path`
- `gzip`
- `numpy`
- `nose.tools`
- `numpy.testing`
- `dicom`


## Step-by-Step Guide

### Step 1: Assign dw_0 = didw.wrapper_from_file(...)

```python
dw_0 = didw.wrapper_from_file(DATA_FILE_B0)
```

**Verification:**
```python
assert_false(z is None)
```

### Step 2: Assign dw_1000 = didw.wrapper_from_data(...)

```python
dw_1000 = didw.wrapper_from_data(DATA)
```

**Verification:**
```python
assert_equal(z, dw_1000.slice_indicator)
```

### Step 3: Assign z = value

```python
z = dw_0.slice_indicator
```

**Verification:**
```python
assert_true(dw_empty.slice_indicator is None)
```

### Step 4: Call assert_false()

```python
assert_false(z is None)
```

### Step 5: Call assert_equal()

```python
assert_equal(z, dw_1000.slice_indicator)
```

### Step 6: Assign dw_empty = didw.Wrapper(...)

```python
dw_empty = didw.Wrapper()
```

### Step 7: Call assert_true()

```python
assert_true(dw_empty.slice_indicator is None)
```


## Complete Example

```python
# Workflow
dw_0 = didw.wrapper_from_file(DATA_FILE_B0)
dw_1000 = didw.wrapper_from_data(DATA)
z = dw_0.slice_indicator
assert_false(z is None)
assert_equal(z, dw_1000.slice_indicator)
dw_empty = didw.Wrapper()
assert_true(dw_empty.slice_indicator is None)
```

## Next Steps


---

*Source: test_dicomwrappers.py:138 | Complexity: Intermediate | Last updated: 2026-05-18*