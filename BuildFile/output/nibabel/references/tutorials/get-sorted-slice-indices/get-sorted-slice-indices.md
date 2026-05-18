# How To: Get Sorted Slice Indices

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get sorted slice indices

## Prerequisites

**Required Modules:**
- `glob`
- `os.path`
- `os.path`
- `warnings`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `fileholders`
- `nifti1`
- `openers`
- `parrec`
- `testing`
- `volumeutils`
- `test_arrayproxy`


## Step-by-Step Guide

### Step 1: Assign hdr = PARRECHeader(...)

```python
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
```

**Verification:**
```python
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices))
```

### Step 2: Assign n_slices = len(...)

```python
n_slices = len(HDR_DEFS)
```

**Verification:**
```python
assert_array_equal(hdr.get_sorted_slice_indices(), [8, 7, 6, 5, 4, 3, 2, 1, 0] + [17, 16, 15, 14, 13, 12, 11, 10, 9] + [26, 25, 24, 23, 22, 21, 20, 19, 18])
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices))
```

**Verification:**
```python
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices - 9))
```

### Step 4: Assign hdr = PARRECHeader(...)

```python
hdr = PARRECHeader(HDR_INFO, HDR_DEFS[::-1])
```

**Verification:**
```python
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices)[::-1])
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(hdr.get_sorted_slice_indices(), [8, 7, 6, 5, 4, 3, 2, 1, 0] + [17, 16, 15, 14, 13, 12, 11, 10, 9] + [26, 25, 24, 23, 22, 21, 20, 19, 18])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices - 9))
```

### Step 7: Assign hdr = PARRECHeader(...)

```python
hdr = PARRECHeader(HDR_INFO, HDR_DEFS[::-1], strict_sort=True)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices)[::-1])
```

### Step 9: Assign hdr = PARRECHeader(...)

```python
hdr = PARRECHeader(HDR_INFO, HDR_DEFS[:-1], permit_truncated=True)
```


## Complete Example

```python
# Workflow
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
n_slices = len(HDR_DEFS)
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices))
hdr = PARRECHeader(HDR_INFO, HDR_DEFS[::-1])
assert_array_equal(hdr.get_sorted_slice_indices(), [8, 7, 6, 5, 4, 3, 2, 1, 0] + [17, 16, 15, 14, 13, 12, 11, 10, 9] + [26, 25, 24, 23, 22, 21, 20, 19, 18])
with clear_and_catch_warnings(modules=[parrec], record=True):
    hdr = PARRECHeader(HDR_INFO, HDR_DEFS[:-1], permit_truncated=True)
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices - 9))
hdr = PARRECHeader(HDR_INFO, HDR_DEFS[::-1], strict_sort=True)
assert_array_equal(hdr.get_sorted_slice_indices(), range(n_slices)[::-1])
```

## Next Steps


---

*Source: test_parrec.py:296 | Complexity: Advanced | Last updated: 2026-05-18*