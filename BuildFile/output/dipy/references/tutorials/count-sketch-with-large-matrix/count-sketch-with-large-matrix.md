# How To: Count Sketch With Large Matrix

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test count_sketch function with a large matrix to check performance.

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `numpy`
- `pytest`
- `dipy.stats.sketching`


## Step-by-Step Guide

### Step 1: 'Test count_sketch function with a large matrix to check performance.'

```python
'Test count_sketch function with a large matrix to check performance.'
```

**Verification:**
```python
assert matrixc.shape == (sketch_rows, matrixa_shape[1]), 'Output shape mismatch for large matrix'
```

### Step 2: Assign matrixa_dtype = value

```python
matrixa_dtype = np.float64
```

### Step 3: Assign matrixa_shape = value

```python
matrixa_shape = (1000, 500)
```

### Step 4: Assign matrixa = np.random.rand(...)

```python
matrixa = np.random.rand(*matrixa_shape)
```

### Step 5: Assign sketch_rows = 50

```python
sketch_rows = 50
```

### Step 6: Assign unknown = matrixa

```python
np.memmap(matrixa_file.name, dtype=matrixa_dtype, mode='w+', shape=matrixa_shape)[:] = matrixa
```

### Step 7: Assign matrixa_name = value

```python
matrixa_name = matrixa_file.name
```

### Step 8: Assign unknown = count_sketch(...)

```python
matrixc_file_name, matrixc_dtype, matrixc_shape = count_sketch(matrixa_name, matrixa_dtype, matrixa_shape, sketch_rows, tmp_dir)
```

### Step 9: Assign matrixc = np.memmap(...)

```python
matrixc = np.memmap(matrixc_file_name, dtype=matrixc_dtype, mode='r+', shape=matrixc_shape)
```

**Verification:**
```python
assert matrixc.shape == (sketch_rows, matrixa_shape[1]), 'Output shape mismatch for large matrix'
```

### Step 10: Call os.unlink()

```python
os.unlink(matrixa_name)
```

### Step 11: Call os.unlink()

```python
os.unlink(matrixc_file_name)
```


## Complete Example

```python
# Workflow
'Test count_sketch function with a large matrix to check performance.'
matrixa_dtype = np.float64
matrixa_shape = (1000, 500)
matrixa = np.random.rand(*matrixa_shape)
with tempfile.NamedTemporaryFile(delete=False, suffix='.mmap') as matrixa_file:
    np.memmap(matrixa_file.name, dtype=matrixa_dtype, mode='w+', shape=matrixa_shape)[:] = matrixa
    matrixa_name = matrixa_file.name
sketch_rows = 50
with tempfile.TemporaryDirectory() as tmp_dir:
    matrixc_file_name, matrixc_dtype, matrixc_shape = count_sketch(matrixa_name, matrixa_dtype, matrixa_shape, sketch_rows, tmp_dir)
    matrixc = np.memmap(matrixc_file_name, dtype=matrixc_dtype, mode='r+', shape=matrixc_shape)
    assert matrixc.shape == (sketch_rows, matrixa_shape[1]), 'Output shape mismatch for large matrix'
    del matrixc
    os.unlink(matrixa_name)
    os.unlink(matrixc_file_name)
```

## Next Steps


---

*Source: test_sketching.py:107 | Complexity: Advanced | Last updated: 2026-05-18*