# How To: Arraysequence Append

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test arraysequence append

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

### Step 1: Assign element = value

```python
element = generate_data(nb_arrays=1, common_shape=SEQ_DATA['seq'].common_shape, rng=SEQ_DATA['rng'])[0]
```

### Step 2: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 3: Call seq.append()

```python
seq.append(element)
```

### Step 4: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'] + [element])
```

### Step 5: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 6: Call seq.append()

```python
seq.append(element.tolist())
```

### Step 7: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'] + [element])
```

### Step 8: Assign seq = ArraySequence(...)

```python
seq = ArraySequence()
```

### Step 9: Call seq.append()

```python
seq.append(element)
```

### Step 10: Call check_arr_seq()

```python
check_arr_seq(seq, [element])
```

### Step 11: Assign seq = unknown.copy(...)

```python
seq = SEQ_DATA['seq'].copy()
```

### Step 12: Call seq.append()

```python
seq.append([])
```

### Step 13: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['seq'])
```

### Step 14: Assign element = value

```python
element = generate_data(nb_arrays=1, common_shape=SEQ_DATA['seq'].common_shape * 2, rng=SEQ_DATA['rng'])[0]
```

### Step 15: Call seq.append()

```python
seq.append(element)
```


## Complete Example

```python
# Workflow
element = generate_data(nb_arrays=1, common_shape=SEQ_DATA['seq'].common_shape, rng=SEQ_DATA['rng'])[0]
seq = SEQ_DATA['seq'].copy()
seq.append(element)
check_arr_seq(seq, SEQ_DATA['data'] + [element])
seq = SEQ_DATA['seq'].copy()
seq.append(element.tolist())
check_arr_seq(seq, SEQ_DATA['data'] + [element])
seq = ArraySequence()
seq.append(element)
check_arr_seq(seq, [element])
seq = SEQ_DATA['seq'].copy()
seq.append([])
check_arr_seq(seq, SEQ_DATA['seq'])
element = generate_data(nb_arrays=1, common_shape=SEQ_DATA['seq'].common_shape * 2, rng=SEQ_DATA['rng'])[0]
with pytest.raises(ValueError):
    seq.append(element)
```

## Next Steps


---

*Source: test_array_sequence.py:142 | Complexity: Advanced | Last updated: 2026-05-18*