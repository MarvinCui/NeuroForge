# How To: Compress Streamlines Memory Leaks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test compress streamlines memory leaks

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `types`
- `warnings`
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `numpy.testing`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.testing.memory`
- `dipy.tracking.streamline`
- `dipy.tracking.streamlinespeed`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign dtypes = value

```python
dtypes = [np.float32, np.float64, np.int32, np.int64]
```

**Verification:**
```python
assert_equal(list_refcount_after, list_refcount_before + 1)
```

### Step 2: Assign NB_STREAMLINES = 10000

```python
NB_STREAMLINES = 10000
```

**Verification:**
```python
assert_equal(list_refcount_after, list_refcount_before + 1)
```

### Step 3: Assign streamlines = value

```python
streamlines = []
```

### Step 4: Assign list_refcount_before = value

```python
list_refcount_before = get_type_refcount()['list']
```

### Step 5: Assign cstreamlines = compress_streamlines(...)

```python
cstreamlines = compress_streamlines(streamlines)
```

### Step 6: Assign list_refcount_after = value

```python
list_refcount_after = get_type_refcount()['list']
```

### Step 7: Call assert_equal()

```python
assert_equal(list_refcount_after, list_refcount_before + 1)
```

### Step 8: Assign s_rng = np.random.default_rng(...)

```python
s_rng = np.random.default_rng(1234)
```

### Step 9: Assign NB_STREAMLINES = 10000

```python
NB_STREAMLINES = 10000
```

### Step 10: Assign streamlines = value

```python
streamlines = [s_rng.standard_normal((s_rng.integers(10, 100), 3)).astype(dtype) for _ in range(NB_STREAMLINES)]
```

### Step 11: Assign list_refcount_before = value

```python
list_refcount_before = get_type_refcount()['list']
```

### Step 12: Assign cstreamlines = compress_streamlines(...)

```python
cstreamlines = compress_streamlines(streamlines)
```

### Step 13: Assign list_refcount_after = value

```python
list_refcount_after = get_type_refcount()['list']
```

### Step 14: Call assert_equal()

```python
assert_equal(list_refcount_after, list_refcount_before + 1)
```

### Step 15: Assign dtype = value

```python
dtype = dtypes[i % len(dtypes)]
```

### Step 16: Call streamlines.append()

```python
streamlines.append(rng.standard_normal((rng.integers(10, 100), 3)).astype(dtype))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
dtypes = [np.float32, np.float64, np.int32, np.int64]
for dtype in dtypes:
    s_rng = np.random.default_rng(1234)
    NB_STREAMLINES = 10000
    streamlines = [s_rng.standard_normal((s_rng.integers(10, 100), 3)).astype(dtype) for _ in range(NB_STREAMLINES)]
    list_refcount_before = get_type_refcount()['list']
    cstreamlines = compress_streamlines(streamlines)
    list_refcount_after = get_type_refcount()['list']
    del cstreamlines
    assert_equal(list_refcount_after, list_refcount_before + 1)
NB_STREAMLINES = 10000
streamlines = []
for i in range(NB_STREAMLINES):
    dtype = dtypes[i % len(dtypes)]
    streamlines.append(rng.standard_normal((rng.integers(10, 100), 3)).astype(dtype))
list_refcount_before = get_type_refcount()['list']
cstreamlines = compress_streamlines(streamlines)
list_refcount_after = get_type_refcount()['list']
assert_equal(list_refcount_after, list_refcount_before + 1)
```

## Next Steps


---

*Source: test_streamline.py:834 | Complexity: Advanced | Last updated: 2026-05-18*