# How To: Slice Indicator

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test slice indicator

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

### Step 1: Assign dw_0 = didw.wrapper_from_file(...)

```python
dw_0 = didw.wrapper_from_file(DATA_FILE_B0)
```

**Verification:**
```python
assert not z is None
```

### Step 2: Assign dw_1000 = didw.wrapper_from_data(...)

```python
dw_1000 = didw.wrapper_from_data(DATA)
```

**Verification:**
```python
assert z == dw_1000.slice_indicator
```

### Step 3: Assign z = value

```python
z = dw_0.slice_indicator
```

**Verification:**
```python
assert dw_empty.slice_indicator is None
```

### Step 4: Assign dw_empty = didw.Wrapper(...)

```python
dw_empty = didw.Wrapper({})
```

**Verification:**
```python
assert dw_empty.slice_indicator is None
```


## Complete Example

```python
# Workflow
dw_0 = didw.wrapper_from_file(DATA_FILE_B0)
dw_1000 = didw.wrapper_from_data(DATA)
z = dw_0.slice_indicator
assert not z is None
assert z == dw_1000.slice_indicator
dw_empty = didw.Wrapper({})
assert dw_empty.slice_indicator is None
```

## Next Steps


---

*Source: test_dicomwrappers.py:301 | Complexity: Intermediate | Last updated: 2026-05-18*