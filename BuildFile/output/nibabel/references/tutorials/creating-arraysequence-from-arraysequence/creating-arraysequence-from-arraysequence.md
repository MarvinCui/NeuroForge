# How To: Creating Arraysequence From Arraysequence

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test creating arraysequence from arraysequence

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

### Step 1: Assign seq = ArraySequence(...)

```python
seq = ArraySequence(SEQ_DATA['data'])
```

### Step 2: Call check_arr_seq()

```python
check_arr_seq(ArraySequence(seq), SEQ_DATA['data'])
```

### Step 3: Assign seq = ArraySequence(...)

```python
seq = ArraySequence()
```

### Step 4: Call check_empty_arr_seq()

```python
check_empty_arr_seq(ArraySequence(seq))
```


## Complete Example

```python
# Workflow
seq = ArraySequence(SEQ_DATA['data'])
check_arr_seq(ArraySequence(seq), SEQ_DATA['data'])
seq = ArraySequence()
check_empty_arr_seq(ArraySequence(seq))
```

## Next Steps


---

*Source: test_array_sequence.py:106 | Complexity: Intermediate | Last updated: 2026-05-18*