# How To: Concatenate

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test concatenate

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

### Step 1: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

**Verification:**
```python
assert new_seq._is_view is not True
```

### Step 2: Assign seqs = value

```python
seqs = [seq[:, [i]] for i in range(seq.common_shape[0])]
```

**Verification:**
```python
assert len(new_seq) == seq.common_shape[0] * len(seq)
```

### Step 3: Assign new_seq = concatenate(...)

```python
new_seq = concatenate(seqs, axis=1)
```

**Verification:**
```python
assert_array_equal(new_seq._data, seq._data.T.reshape((-1, 1)))
```

### Step 4: Call check_arr_seq()

```python
check_arr_seq(new_seq, SEQ_DATA['data'])
```

**Verification:**
```python
assert new_seq._is_view is not True
```

### Step 5: Assign seq = value

```python
seq = SEQ_DATA['seq']
```

### Step 6: Assign seqs = value

```python
seqs = [seq[:, [i]] for i in range(seq.common_shape[0])]
```

### Step 7: Assign new_seq = concatenate(...)

```python
new_seq = concatenate(seqs, axis=0)
```

**Verification:**
```python
assert len(new_seq) == seq.common_shape[0] * len(seq)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(new_seq._data, seq._data.T.reshape((-1, 1)))
```


## Complete Example

```python
# Workflow
seq = SEQ_DATA['seq'].copy()
seqs = [seq[:, [i]] for i in range(seq.common_shape[0])]
new_seq = concatenate(seqs, axis=1)
seq._data += 100
check_arr_seq(new_seq, SEQ_DATA['data'])
assert new_seq._is_view is not True
seq = SEQ_DATA['seq']
seqs = [seq[:, [i]] for i in range(seq.common_shape[0])]
new_seq = concatenate(seqs, axis=0)
assert len(new_seq) == seq.common_shape[0] * len(seq)
assert_array_equal(new_seq._data, seq._data.T.reshape((-1, 1)))
```

## Next Steps


---

*Source: test_array_sequence.py:507 | Complexity: Advanced | Last updated: 2026-05-18*