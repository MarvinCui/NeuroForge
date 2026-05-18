# How To: Count Sketch Randomness

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if count_sketch produces different results with different random seeds.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `tempfile`
- `numpy`
- `pytest`
- `dipy.stats.sketching`

**Setup Required:**
```python
# Fixtures: setup_matrices
```

## Step-by-Step Guide

### Step 1: 'Test if count_sketch produces different results with different random seeds.'

```python
'Test if count_sketch produces different results with different random seeds.'
```

**Verification:**
```python
assert not np.allclose(matrixc_1, matrixc_2), 'Sketches should differ with different random seeds'
```

### Step 2: Assign unknown = setup_matrices

```python
matrixa_name, matrixa_dtype, matrixa_shape = setup_matrices
```

### Step 3: Assign sketch_rows = 10

```python
sketch_rows = 10
```

### Step 4: Call np.random.seed()

```python
np.random.seed(42)
```

### Step 5: Assign unknown = count_sketch(...)

```python
matrixc_file_name_1, _, _ = count_sketch(matrixa_name, matrixa_dtype, matrixa_shape, sketch_rows, tmp_dir)
```

### Step 6: Assign matrixc_1 = np.memmap(...)

```python
matrixc_1 = np.memmap(matrixc_file_name_1, dtype=matrixa_dtype, mode='r+')
```

### Step 7: Call np.random.seed()

```python
np.random.seed(43)
```

### Step 8: Assign unknown = count_sketch(...)

```python
matrixc_file_name_2, _, _ = count_sketch(matrixa_name, matrixa_dtype, matrixa_shape, sketch_rows, tmp_dir)
```

### Step 9: Assign matrixc_2 = np.memmap(...)

```python
matrixc_2 = np.memmap(matrixc_file_name_2, dtype=matrixa_dtype, mode='r+')
```

**Verification:**
```python
assert not np.allclose(matrixc_1, matrixc_2), 'Sketches should differ with different random seeds'
```

### Step 10: Call os.unlink()

```python
os.unlink(matrixc_file_name_1)
```

### Step 11: Call os.unlink()

```python
os.unlink(matrixc_file_name_2)
```


## Complete Example

```python
# Setup
# Fixtures: setup_matrices

# Workflow
'Test if count_sketch produces different results with different random seeds.'
matrixa_name, matrixa_dtype, matrixa_shape = setup_matrices
sketch_rows = 10
with tempfile.TemporaryDirectory() as tmp_dir:
    np.random.seed(42)
    matrixc_file_name_1, _, _ = count_sketch(matrixa_name, matrixa_dtype, matrixa_shape, sketch_rows, tmp_dir)
    matrixc_1 = np.memmap(matrixc_file_name_1, dtype=matrixa_dtype, mode='r+')
    np.random.seed(43)
    matrixc_file_name_2, _, _ = count_sketch(matrixa_name, matrixa_dtype, matrixa_shape, sketch_rows, tmp_dir)
    matrixc_2 = np.memmap(matrixc_file_name_2, dtype=matrixa_dtype, mode='r+')
    assert not np.allclose(matrixc_1, matrixc_2), 'Sketches should differ with different random seeds'
    del matrixc_1
    del matrixc_2
    os.unlink(matrixc_file_name_1)
    os.unlink(matrixc_file_name_2)
```

## Next Steps


---

*Source: test_sketching.py:56 | Complexity: Advanced | Last updated: 2026-05-18*