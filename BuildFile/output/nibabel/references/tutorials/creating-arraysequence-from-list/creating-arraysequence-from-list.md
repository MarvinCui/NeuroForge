# How To: Creating Arraysequence From List

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test creating arraysequence from list

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

### Step 1: Call check_empty_arr_seq()

```python
check_empty_arr_seq(ArraySequence([]))
```

### Step 2: Assign N = 5

```python
N = 5
```

### Step 3: Assign buffer_size = value

```python
buffer_size = 1.0 / 1024 ** 2
```

### Step 4: Call check_arr_seq()

```python
check_arr_seq(ArraySequence(iter(SEQ_DATA['data']), buffer_size), SEQ_DATA['data'])
```

### Step 5: Assign common_shape = tuple(...)

```python
common_shape = tuple((SEQ_DATA['rng'].randint(1, 10) for _ in range(ndim - 1)))
```

### Step 6: Assign data = generate_data(...)

```python
data = generate_data(nb_arrays=5, common_shape=common_shape, rng=SEQ_DATA['rng'])
```

### Step 7: Call check_arr_seq()

```python
check_arr_seq(ArraySequence(data), data)
```


## Complete Example

```python
# Workflow
check_empty_arr_seq(ArraySequence([]))
N = 5
for ndim in range(1, N + 1):
    common_shape = tuple((SEQ_DATA['rng'].randint(1, 10) for _ in range(ndim - 1)))
    data = generate_data(nb_arrays=5, common_shape=common_shape, rng=SEQ_DATA['rng'])
    check_arr_seq(ArraySequence(data), data)
buffer_size = 1.0 / 1024 ** 2
check_arr_seq(ArraySequence(iter(SEQ_DATA['data']), buffer_size), SEQ_DATA['data'])
```

## Next Steps


---

*Source: test_array_sequence.py:75 | Complexity: Intermediate | Last updated: 2026-05-18*