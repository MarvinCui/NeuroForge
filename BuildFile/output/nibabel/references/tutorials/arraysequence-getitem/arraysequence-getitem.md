# How To: Arraysequence Getitem

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test arraysequence getitem

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

### Step 1: Assign indices = list(...)

```python
indices = list(range(len(SEQ_DATA['seq'])))
```

**Verification:**
```python
assert_array_equal(SEQ_DATA['seq'][i], e)
```

### Step 2: Assign seq_view = value

```python
seq_view = SEQ_DATA['seq'][indices]
```

### Step 3: Call check_arr_seq_view()

```python
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
```

### Step 4: Call check_arr_seq()

```python
check_arr_seq(seq_view, SEQ_DATA['seq'])
```

### Step 5: Call unknown.shuffle()

```python
SEQ_DATA['rng'].shuffle(indices)
```

### Step 6: Assign seq_view = value

```python
seq_view = SEQ_DATA['seq'][indices]
```

### Step 7: Call check_arr_seq_view()

```python
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
```

### Step 8: Call check_arr_seq()

```python
check_arr_seq(seq_view, [SEQ_DATA['data'][i] for i in indices])
```

### Step 9: Assign seq_view = value

```python
seq_view = SEQ_DATA['seq'][::2]
```

### Step 10: Call check_arr_seq_view()

```python
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
```

### Step 11: Call check_arr_seq()

```python
check_arr_seq(seq_view, SEQ_DATA['data'][::2])
```

### Step 12: Assign selection = np.array(...)

```python
selection = np.array([False, True, True, False, True])
```

### Step 13: Assign seq_view = value

```python
seq_view = SEQ_DATA['seq'][selection]
```

### Step 14: Call check_arr_seq_view()

```python
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
```

### Step 15: Call check_arr_seq()

```python
check_arr_seq(seq_view, [SEQ_DATA['data'][i] for i, keep in enumerate(selection) if keep])
```

### Step 16: Assign seq_view = value

```python
seq_view = SEQ_DATA['seq'][:, 2]
```

### Step 17: Call check_arr_seq_view()

```python
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
```

### Step 18: Call check_arr_seq()

```python
check_arr_seq(seq_view, [d[:, 2] for d in SEQ_DATA['data']])
```

### Step 19: Assign seq_view = value

```python
seq_view = SEQ_DATA['seq'][::-2][:, 2]
```

### Step 20: Call check_arr_seq_view()

```python
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
```

### Step 21: Call check_arr_seq()

```python
check_arr_seq(seq_view, [d[:, 2] for d in SEQ_DATA['data'][::-2]])
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(SEQ_DATA['seq'][i], e)
```

### Step 23: Assign seq_view = value

```python
seq_view = SEQ_DATA['seq'][np.array(indices, dtype=dtype)]
```

### Step 24: Call check_arr_seq_view()

```python
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
```

### Step 25: Call check_arr_seq()

```python
check_arr_seq(seq_view, SEQ_DATA['seq'])
```

### Step 26: SEQ_DATA['seq']['abc']

```python
SEQ_DATA['seq']['abc']
```


## Complete Example

```python
# Workflow
for i, e in enumerate(SEQ_DATA['seq']):
    assert_array_equal(SEQ_DATA['seq'][i], e)
indices = list(range(len(SEQ_DATA['seq'])))
seq_view = SEQ_DATA['seq'][indices]
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
check_arr_seq(seq_view, SEQ_DATA['seq'])
for dtype in [np.int8, np.int16, np.int32, np.int64]:
    seq_view = SEQ_DATA['seq'][np.array(indices, dtype=dtype)]
    check_arr_seq_view(seq_view, SEQ_DATA['seq'])
    check_arr_seq(seq_view, SEQ_DATA['seq'])
SEQ_DATA['rng'].shuffle(indices)
seq_view = SEQ_DATA['seq'][indices]
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
check_arr_seq(seq_view, [SEQ_DATA['data'][i] for i in indices])
seq_view = SEQ_DATA['seq'][::2]
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
check_arr_seq(seq_view, SEQ_DATA['data'][::2])
selection = np.array([False, True, True, False, True])
seq_view = SEQ_DATA['seq'][selection]
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
check_arr_seq(seq_view, [SEQ_DATA['data'][i] for i, keep in enumerate(selection) if keep])
with pytest.raises(TypeError):
    SEQ_DATA['seq']['abc']
seq_view = SEQ_DATA['seq'][:, 2]
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
check_arr_seq(seq_view, [d[:, 2] for d in SEQ_DATA['data']])
seq_view = SEQ_DATA['seq'][::-2][:, 2]
check_arr_seq_view(seq_view, SEQ_DATA['seq'])
check_arr_seq(seq_view, [d[:, 2] for d in SEQ_DATA['data'][::-2]])
```

## Next Steps


---

*Source: test_array_sequence.py:225 | Complexity: Advanced | Last updated: 2026-05-18*