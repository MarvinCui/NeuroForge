# How To: Arraysequence Copy

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test arraysequence copy

## Prerequisites

**Required Modules:**
- `itertools`
- `os`
- `tempfile`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `array_sequence`


## Step-by-Step Guide

### Step 1: Assign orig = value

```python
orig = SEQ_DATA['seq']
```

**Verification:**
```python
assert n_rows == orig.total_nb_rows
```

### Step 2: Assign seq = orig.copy(...)

```python
seq = orig.copy()
```

**Verification:**
```python
assert_array_equal(seq._data, orig._data[:n_rows])
```

### Step 3: Assign n_rows = value

```python
n_rows = seq.total_nb_rows
```

**Verification:**
```python
assert seq._data is not orig._data
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(seq._data, orig._data[:n_rows])
```

**Verification:**
```python
assert_array_equal(seq._offsets, orig._offsets)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(seq._offsets, orig._offsets)
```

**Verification:**
```python
assert seq._offsets is not orig._offsets
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(seq._lengths, orig._lengths)
```

**Verification:**
```python
assert_array_equal(seq._lengths, orig._lengths)
```

### Step 7: Assign seq = unknown.copy(...)

```python
seq = orig[::2].copy()
```

**Verification:**
```python
assert seq._lengths is not orig._lengths
```

### Step 8: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'][::2])
```

**Verification:**
```python
assert seq.common_shape == orig.common_shape
```


## Complete Example

```python
# Workflow
orig = SEQ_DATA['seq']
seq = orig.copy()
n_rows = seq.total_nb_rows
assert n_rows == orig.total_nb_rows
assert_array_equal(seq._data, orig._data[:n_rows])
assert seq._data is not orig._data
assert_array_equal(seq._offsets, orig._offsets)
assert seq._offsets is not orig._offsets
assert_array_equal(seq._lengths, orig._lengths)
assert seq._lengths is not orig._lengths
assert seq.common_shape == orig.common_shape
seq = orig[::2].copy()
check_arr_seq(seq, SEQ_DATA['data'][::2])
assert seq._data is not orig._data
```

## Next Steps


---

*Source: test_array_sequence.py:123 | Complexity: Advanced | Last updated: 2026-05-18*