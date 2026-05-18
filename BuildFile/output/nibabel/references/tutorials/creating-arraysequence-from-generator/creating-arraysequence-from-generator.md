# How To: Creating Arraysequence From Generator

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test creating arraysequence from generator

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

### Step 1: Assign unknown = itertools.tee(...)

```python
gen_1, gen_2 = itertools.tee((e for e in SEQ_DATA['data']))
```

**Verification:**
```python
assert seq_with_buffer.get_data().shape == seq.get_data().shape
```

### Step 2: Assign seq = ArraySequence(...)

```python
seq = ArraySequence(gen_1)
```

**Verification:**
```python
assert seq_with_buffer._buffer_size > seq._buffer_size
```

### Step 3: Assign seq_with_buffer = ArraySequence(...)

```python
seq_with_buffer = ArraySequence(gen_2, buffer_size=256)
```

**Verification:**
```python
assert seq_with_buffer.get_data().shape == seq.get_data().shape
```

### Step 4: Call check_arr_seq()

```python
check_arr_seq(seq, SEQ_DATA['data'])
```

### Step 5: Call check_arr_seq()

```python
check_arr_seq(seq_with_buffer, SEQ_DATA['data'])
```

### Step 6: Call check_empty_arr_seq()

```python
check_empty_arr_seq(ArraySequence(gen_1))
```


## Complete Example

```python
# Workflow
gen_1, gen_2 = itertools.tee((e for e in SEQ_DATA['data']))
seq = ArraySequence(gen_1)
seq_with_buffer = ArraySequence(gen_2, buffer_size=256)
assert seq_with_buffer.get_data().shape == seq.get_data().shape
assert seq_with_buffer._buffer_size > seq._buffer_size
check_arr_seq(seq, SEQ_DATA['data'])
check_arr_seq(seq_with_buffer, SEQ_DATA['data'])
check_empty_arr_seq(ArraySequence(gen_1))
```

## Next Steps


---

*Source: test_array_sequence.py:90 | Complexity: Intermediate | Last updated: 2026-05-18*