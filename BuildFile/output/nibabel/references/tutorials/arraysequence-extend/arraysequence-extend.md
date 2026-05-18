# How To: Arraysequence Extend

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test arraysequence extend

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

### Step 1: Assign new_data = generate_data(...)

```python
new_data = generate_data(nb_arrays=10, common_shape=SEQ_DATA['seq'].common_shape, rng=SEQ_DATA['rng'])
```

### Step 2: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 3: Call seq.extend()

```python
seq.extend([])
```

### Step 4: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'])
```

### Step 5: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 6: Call seq.extend()

```python
seq.extend(new_data)
```

### Step 7: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'] + new_data)
```

### Step 8: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 9: Call seq.extend()

```python
seq.extend((d for d in new_data))
```

### Step 10: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'] + new_data)
```

### Step 11: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 12: Call seq.extend()

```python
seq.extend(ArraySequence(new_data))
```

### Step 13: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'] + new_data)
```

### Step 14: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 15: Call seq.extend()

```python
seq.extend(ArraySequence(new_data)[::2])
```

### Step 16: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'] + new_data[::2])
```

### Step 17: Assign seq = ArraySequence(...)

```python
seq = ArraySequence()
```

### Step 18: Call seq.extend()

```python
seq.extend(ArraySequence())
```

### Step 19: Call check_empty_arr_seq()

```python
check_empty_arr_seq(seq)
```

### Step 20: Call seq.extend()

```python
seq.extend(SEQ_DATA['seq'])
```

### Step 21: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'])
```

### Step 22: Assign data = generate_data(...)

```python
data = generate_data(nb_arrays=10, common_shape=SEQ_DATA['seq'].common_shape * 2, rng=SEQ_DATA['rng'])
```

### Step 23: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 24: Assign _ = value

```python
_ = seq[:2]
```

### Step 25: Call seq.extend()

```python
seq.extend(ArraySequence(new_data))
```

### Step 26: Call seq.extend()

```python
seq.extend(data)
```


## Complete Example

```python
# Workflow
new_data = generate_data(nb_arrays=10, common_shape=SEQ_DATA['seq'].common_shape, rng=SEQ_DATA['rng'])
seq = SEQ_DATA['seq'].copy()
seq.extend([])
check_arr_seq(seq, SEQ_DATA['data'])
seq = SEQ_DATA['seq'].copy()
seq.extend(new_data)
check_arr_seq(seq, SEQ_DATA['data'] + new_data)
seq = SEQ_DATA['seq'].copy()
seq.extend((d for d in new_data))
check_arr_seq(seq, SEQ_DATA['data'] + new_data)
seq = SEQ_DATA['seq'].copy()
seq.extend(ArraySequence(new_data))
check_arr_seq(seq, SEQ_DATA['data'] + new_data)
seq = SEQ_DATA['seq'].copy()
seq.extend(ArraySequence(new_data)[::2])
check_arr_seq(seq, SEQ_DATA['data'] + new_data[::2])
seq = ArraySequence()
seq.extend(ArraySequence())
check_empty_arr_seq(seq)
seq.extend(SEQ_DATA['seq'])
check_arr_seq(seq, SEQ_DATA['data'])
data = generate_data(nb_arrays=10, common_shape=SEQ_DATA['seq'].common_shape * 2, rng=SEQ_DATA['rng'])
seq = SEQ_DATA['seq'].copy()
with pytest.raises(ValueError):
    seq.extend(data)
_ = seq[:2]
seq.extend(ArraySequence(new_data))
```

## Next Steps


---

*Source: test_array_sequence.py:174 | Complexity: Advanced | Last updated: 2026-05-18*