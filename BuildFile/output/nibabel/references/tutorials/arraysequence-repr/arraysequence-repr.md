# How To: Arraysequence Repr

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test arraysequence repr

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

### Step 1: Call repr()

```python
repr(SEQ_DATA['seq'])
```

**Verification:**
```python
assert len(txt2) < len(txt1)
```

### Step 2: Assign nb_arrays = 50

```python
nb_arrays = 50
```

### Step 3: Assign seq = ArraySequence(...)

```python
seq = ArraySequence(generate_data(nb_arrays, common_shape=(1,), rng=SEQ_DATA['rng']))
```

### Step 4: Assign bkp_threshold = value

```python
bkp_threshold = np.get_printoptions()['threshold']
```

### Step 5: Call np.set_printoptions()

```python
np.set_printoptions(threshold=nb_arrays * 2)
```

### Step 6: Assign txt1 = repr(...)

```python
txt1 = repr(seq)
```

### Step 7: Call np.set_printoptions()

```python
np.set_printoptions(threshold=nb_arrays // 2)
```

### Step 8: Assign txt2 = repr(...)

```python
txt2 = repr(seq)
```

**Verification:**
```python
assert len(txt2) < len(txt1)
```

### Step 9: Call np.set_printoptions()

```python
np.set_printoptions(threshold=bkp_threshold)
```


## Complete Example

```python
# Workflow
repr(SEQ_DATA['seq'])
nb_arrays = 50
seq = ArraySequence(generate_data(nb_arrays, common_shape=(1,), rng=SEQ_DATA['rng']))
bkp_threshold = np.get_printoptions()['threshold']
np.set_printoptions(threshold=nb_arrays * 2)
txt1 = repr(seq)
np.set_printoptions(threshold=nb_arrays // 2)
txt2 = repr(seq)
assert len(txt2) < len(txt1)
np.set_printoptions(threshold=bkp_threshold)
```

## Next Steps


---

*Source: test_array_sequence.py:456 | Complexity: Advanced | Last updated: 2026-05-18*