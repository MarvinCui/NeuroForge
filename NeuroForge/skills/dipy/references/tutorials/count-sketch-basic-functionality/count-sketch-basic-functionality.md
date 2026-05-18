# How To: Count Sketch Basic Functionality

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the basic functionality of the count_sketch function.

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

### Step 1: 'Test the basic functionality of the count_sketch function.'

```python
'Test the basic functionality of the count_sketch function.'
```

**Verification:**
```python
assert matrixc.shape == (sketch_rows, matrixa_shape[1]), 'Output shape mismatch'
```

### Step 2: Assign unknown = setup_matrices

```python
matrixa_name, matrixa_dtype, matrixa_shape = setup_matrices
```

**Verification:**
```python
assert matrixc.dtype == matrixa_dtype, 'Output dtype mismatch'
```

### Step 3: Assign sketch_rows = 10

```python
sketch_rows = 10
```

### Step 4: Assign unknown = count_sketch(...)

```python
matrixc_file_name, matrixc_dtype, matrixc_shape = count_sketch(matrixa_name, matrixa_dtype, matrixa_shape, sketch_rows, tmp_dir)
```

### Step 5: Assign matrixc = np.memmap(...)

```python
matrixc = np.memmap(matrixc_file_name, dtype=matrixc_dtype, mode='r+', shape=matrixc_shape)
```

**Verification:**
```python
assert matrixc.shape == (sketch_rows, matrixa_shape[1]), 'Output shape mismatch'
```

### Step 6: Call os.unlink()

```python
os.unlink(matrixc_file_name)
```


## Complete Example

```python
# Setup
# Fixtures: setup_matrices

# Workflow
'Test the basic functionality of the count_sketch function.'
matrixa_name, matrixa_dtype, matrixa_shape = setup_matrices
sketch_rows = 10
with tempfile.TemporaryDirectory() as tmp_dir:
    matrixc_file_name, matrixc_dtype, matrixc_shape = count_sketch(matrixa_name, matrixa_dtype, matrixa_shape, sketch_rows, tmp_dir)
    matrixc = np.memmap(matrixc_file_name, dtype=matrixc_dtype, mode='r+', shape=matrixc_shape)
    assert matrixc.shape == (sketch_rows, matrixa_shape[1]), 'Output shape mismatch'
    assert matrixc.dtype == matrixa_dtype, 'Output dtype mismatch'
    del matrixc
    os.unlink(matrixc_file_name)
```

## Next Steps


---

*Source: test_sketching.py:31 | Complexity: Intermediate | Last updated: 2026-05-18*