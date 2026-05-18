# How To: Vol Matching

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test vol matching

## Prerequisites

**Required Modules:**
- `gzip`
- `copy`
- `decimal`
- `hashlib`
- `os.path`
- `os.path`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `openers`
- `tests.nibabel_data`
- `volumeutils`


## Step-by-Step Guide

### Step 1: Assign dw_siemens = didw.wrapper_from_data(...)

```python
dw_siemens = didw.wrapper_from_data(DATA)
```

**Verification:**
```python
assert dw_siemens.is_mosaic
```

### Step 2: Assign dw_plain = didw.Wrapper(...)

```python
dw_plain = didw.Wrapper(DATA)
```

**Verification:**
```python
assert dw_siemens.is_csa
```

### Step 3: Assign dw_empty = didw.Wrapper(...)

```python
dw_empty = didw.Wrapper({})
```

**Verification:**
```python
assert dw_siemens.is_same_series(dw_siemens)
```

### Step 4: Assign dw_philips = didw.wrapper_from_data(...)

```python
dw_philips = didw.wrapper_from_data(DATA_PHILIPS)
```

**Verification:**
```python
assert not dw_plain.is_mosaic
```

### Step 5: Assign dw_plain_philips = didw.Wrapper(...)

```python
dw_plain_philips = didw.Wrapper(DATA)
```

**Verification:**
```python
assert not dw_plain.is_csa
```

### Step 6: Assign dw_empty = didw.Wrapper(...)

```python
dw_empty = didw.Wrapper({})
```

**Verification:**
```python
assert dw_plain.is_same_series(dw_plain)
```

### Step 7: Assign series_signature = value

```python
series_signature = {}
```

**Verification:**
```python
assert not dw_plain.is_same_series(dw_siemens)
```


## Complete Example

```python
# Workflow
dw_siemens = didw.wrapper_from_data(DATA)
assert dw_siemens.is_mosaic
assert dw_siemens.is_csa
assert dw_siemens.is_same_series(dw_siemens)
dw_plain = didw.Wrapper(DATA)
assert not dw_plain.is_mosaic
assert not dw_plain.is_csa
assert dw_plain.is_same_series(dw_plain)
assert not dw_plain.is_same_series(dw_siemens)
assert not dw_siemens.is_same_series(dw_plain)
dw_empty = didw.Wrapper({})
assert dw_empty.is_same_series(dw_empty)
assert not dw_empty.is_same_series(dw_plain)
assert not dw_plain.is_same_series(dw_empty)

class C:
    series_signature = {}
assert dw_empty.is_same_series(C())
dw_philips = didw.wrapper_from_data(DATA_PHILIPS)
assert dw_philips.is_multiframe
assert dw_philips.is_same_series(dw_philips)
dw_plain_philips = didw.Wrapper(DATA)
assert not dw_plain_philips.is_multiframe
assert dw_plain_philips.is_same_series(dw_plain_philips)
assert not dw_plain_philips.is_same_series(dw_philips)
assert not dw_philips.is_same_series(dw_plain_philips)
dw_empty = didw.Wrapper({})
assert dw_empty.is_same_series(dw_empty)
assert not dw_empty.is_same_series(dw_plain_philips)
assert not dw_plain_philips.is_same_series(dw_empty)
```

## Next Steps


---

*Source: test_dicomwrappers.py:249 | Complexity: Intermediate | Last updated: 2026-05-18*