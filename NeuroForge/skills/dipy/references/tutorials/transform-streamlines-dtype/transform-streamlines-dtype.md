# How To: Transform Streamlines Dtype

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test transform streamlines dtype

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign identity = np.eye(...)

```python
identity = np.eye(4)
```

**Verification:**
```python
assert_equal(data_dtype, streamlines._data.dtype)
```

### Step 2: Assign streamlines = Streamlines(...)

```python
streamlines = Streamlines([streamline])
```

**Verification:**
```python
assert_equal(offsets_dtype, streamlines._offsets.dtype)
```

### Step 3: Assign streamlines._data = streamlines._data.astype(...)

```python
streamlines._data = streamlines._data.astype(np.float16)
```

### Step 4: Assign data_dtype = value

```python
data_dtype = streamlines._data.dtype
```

### Step 5: Assign offsets_dtype = value

```python
offsets_dtype = streamlines._offsets.dtype
```

### Step 6: Assign streamlines = transform_streamlines(...)

```python
streamlines = transform_streamlines(streamlines, identity, in_place=False)
```

### Step 7: Call assert_equal()

```python
assert_equal(data_dtype, streamlines._data.dtype)
```

### Step 8: Call assert_equal()

```python
assert_equal(offsets_dtype, streamlines._offsets.dtype)
```


## Complete Example

```python
# Workflow
identity = np.eye(4)
streamlines = Streamlines([streamline])
streamlines._data = streamlines._data.astype(np.float16)
data_dtype = streamlines._data.dtype
offsets_dtype = streamlines._offsets.dtype
streamlines = transform_streamlines(streamlines, identity, in_place=False)
assert_equal(data_dtype, streamlines._data.dtype)
assert_equal(offsets_dtype, streamlines._offsets.dtype)
```

## Next Steps


---

*Source: test_streamline.py:565 | Complexity: Advanced | Last updated: 2026-05-18*