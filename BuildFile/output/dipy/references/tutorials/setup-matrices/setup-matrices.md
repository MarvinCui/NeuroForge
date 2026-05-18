# How To: Setup Matrices

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Fixture to set up matrix A as a memmap file and return its details.

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `numpy`
- `pytest`
- `dipy.stats.sketching`


## Step-by-Step Guide

### Step 1: 'Fixture to set up matrix A as a memmap file and return its details.'

```python
'Fixture to set up matrix A as a memmap file and return its details.'
```

### Step 2: Assign matrixa_dtype = value

```python
matrixa_dtype = np.float64
```

### Step 3: Assign matrixa_shape = value

```python
matrixa_shape = (100, 50)
```

### Step 4: Assign matrixa = np.random.rand(...)

```python
matrixa = np.random.rand(*matrixa_shape)
```

### Step 5: yield (matrixa_file_name, matrixa_dtype, matrixa_shape)

```python
yield (matrixa_file_name, matrixa_dtype, matrixa_shape)
```

### Step 6: Call os.unlink()

```python
os.unlink(matrixa_file_name)
```

### Step 7: Assign unknown = matrixa

```python
np.memmap(matrixa_file.name, dtype=matrixa_dtype, mode='w+', shape=matrixa_shape)[:] = matrixa
```

### Step 8: Assign matrixa_file_name = value

```python
matrixa_file_name = matrixa_file.name
```


## Complete Example

```python
# Workflow
'Fixture to set up matrix A as a memmap file and return its details.'
matrixa_dtype = np.float64
matrixa_shape = (100, 50)
matrixa = np.random.rand(*matrixa_shape)
with tempfile.NamedTemporaryFile(delete=False, suffix='.mmap') as matrixa_file:
    np.memmap(matrixa_file.name, dtype=matrixa_dtype, mode='w+', shape=matrixa_shape)[:] = matrixa
    matrixa_file_name = matrixa_file.name
yield (matrixa_file_name, matrixa_dtype, matrixa_shape)
os.unlink(matrixa_file_name)
```

## Next Steps


---

*Source: test_sketching.py:11 | Complexity: Advanced | Last updated: 2026-05-18*