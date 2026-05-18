# How To: Write Morph Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: Test write_morph_data edge cases

## Prerequisites

**Required Modules:**
- `getpass`
- `hashlib`
- `os`
- `struct`
- `time`
- `unittest`
- `os.path`
- `os.path`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileslice`
- `testing`
- `tests.nibabel_data`
- `tmpdirs`
- `io`


## Step-by-Step Guide

### Step 1: 'Test write_morph_data edge cases'

```python
'Test write_morph_data edge cases'
```

**Verification:**
```python
assert np.array_equal(read_morph_data('test.curv'), values)
```

### Step 2: Assign values = np.arange(...)

```python
values = np.arange(20, dtype='>f4')
```

### Step 3: Assign okay_shapes = value

```python
okay_shapes = [(20,), (20, 1), (20, 1, 1), (1, 20)]
```

### Step 4: Assign bad_shapes = value

```python
bad_shapes = [(10, 2), (1, 1, 20, 1, 1)]
```

### Step 5: Assign big_num = value

```python
big_num = np.iinfo('i4').max + 1
```

### Step 6: Call write_morph_data()

```python
write_morph_data('test.curv', values.reshape(shape))
```

**Verification:**
```python
assert np.array_equal(read_morph_data('test.curv'), values)
```

### Step 7: Call write_morph_data()

```python
write_morph_data('test.curv', np.zeros(shape), big_num)
```

### Step 8: Call write_morph_data()

```python
write_morph_data('test.curv', strided_scalar((big_num,)))
```

### Step 9: Call write_morph_data()

```python
write_morph_data('test.curv', values.reshape(shape))
```


## Complete Example

```python
# Workflow
'Test write_morph_data edge cases'
values = np.arange(20, dtype='>f4')
okay_shapes = [(20,), (20, 1), (20, 1, 1), (1, 20)]
bad_shapes = [(10, 2), (1, 1, 20, 1, 1)]
big_num = np.iinfo('i4').max + 1
with InTemporaryDirectory():
    for shape in okay_shapes:
        write_morph_data('test.curv', values.reshape(shape))
        assert np.array_equal(read_morph_data('test.curv'), values)
    with pytest.raises(ValueError):
        write_morph_data('test.curv', np.zeros(shape), big_num)
    if np.dtype(int) != np.dtype(np.int32):
        with pytest.raises(ValueError):
            write_morph_data('test.curv', strided_scalar((big_num,)))
    for shape in bad_shapes:
        with pytest.raises(ValueError):
            write_morph_data('test.curv', values.reshape(shape))
```

## Next Steps


---

*Source: test_io.py:151 | Complexity: Advanced | Last updated: 2026-05-18*