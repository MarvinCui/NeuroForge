# How To: As Ndarray Memmap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test as ndarray memmap

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `nilearn._utils.numpy_conversions`


## Step-by-Step Guide

### Step 1: Assign filename = value

```python
filename = Path(__file__).parent / 'data' / 'mmap.dat'
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 2: Assign arr1 = np.memmap(...)

```python
arr1 = np.memmap(filename, dtype='float32', mode='w+', shape=(5,))
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 3: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1)
```

**Verification:**
```python
assert arr2.dtype == int
```

### Step 4: Assign arr1 = np.memmap(...)

```python
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 5: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, copy=True)
```

**Verification:**
```python
assert arr2.dtype == np.float32
```

### Step 6: Assign arr1 = np.memmap(...)

```python
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
```

**Verification:**
```python
assert not are_arrays_identical(arr1, arr2)
```

### Step 7: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, dtype=int)
```

**Verification:**
```python
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
```

### Step 8: Assign arr1 = np.memmap(...)

```python
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
```

**Verification:**
```python
assert arr2.dtype == arr1.dtype
```

### Step 9: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, dtype=np.float32)
```

**Verification:**
```python
assert not are_arrays_identical(arr1[0], arr2[0])
```

### Step 10: Assign arr1 = np.memmap(...)

```python
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10))
```

**Verification:**
```python
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
```

### Step 11: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, order='F')
```

**Verification:**
```python
assert arr2.dtype == arr1.dtype
```

### Step 12: Assign arr1 = np.memmap(...)

```python
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10), order='F')
```

**Verification:**
```python
assert not are_arrays_identical(arr1[0], arr2[0])
```

### Step 13: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, order='F')
```

**Verification:**
```python
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
```

### Step 14: Assign arr1 = np.memmap(...)

```python
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10), order='F')
```

**Verification:**
```python
assert arr2.dtype == np.int32
```

### Step 15: Assign arr2 = as_ndarray(...)

```python
arr2 = as_ndarray(arr1, order='F', dtype=np.int32)
```

**Verification:**
```python
assert not are_arrays_identical(arr1[0], arr2[0])
```


## Complete Example

```python
# Workflow
filename = Path(__file__).parent / 'data' / 'mmap.dat'
arr1 = np.memmap(filename, dtype='float32', mode='w+', shape=(5,))
arr2 = as_ndarray(arr1)
assert not are_arrays_identical(arr1, arr2)
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
arr2 = as_ndarray(arr1, copy=True)
assert not are_arrays_identical(arr1, arr2)
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
arr2 = as_ndarray(arr1, dtype=int)
assert arr2.dtype == int
assert not are_arrays_identical(arr1, arr2)
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
arr2 = as_ndarray(arr1, dtype=np.float32)
assert arr2.dtype == np.float32
assert not are_arrays_identical(arr1, arr2)
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10))
arr2 = as_ndarray(arr1, order='F')
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
assert arr2.dtype == arr1.dtype
assert not are_arrays_identical(arr1[0], arr2[0])
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10), order='F')
arr2 = as_ndarray(arr1, order='F')
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
assert arr2.dtype == arr1.dtype
assert not are_arrays_identical(arr1[0], arr2[0])
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10), order='F')
arr2 = as_ndarray(arr1, order='F', dtype=np.int32)
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
assert arr2.dtype == np.int32
assert not are_arrays_identical(arr1[0], arr2[0])
```

## Next Steps


---

*Source: test_numpy_conversions.py:148 | Complexity: Advanced | Last updated: 2026-05-18*