# How To: Array From File

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test array from file

## Prerequisites

**Required Modules:**
- `__future__`
- `py3k`
- `tempfile`
- `numpy`
- `tmpdirs`
- `volumeutils`
- `casting`
- `numpy.testing`
- `nose.tools`
- `testing`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (2, 3, 4)
```

**Verification:**
```python
assert_true(buf_chk(in_arr, BytesIO(), None, offset))
```

### Step 2: Assign dtype = np.dtype(...)

```python
dtype = np.dtype(np.float32)
```

**Verification:**
```python
assert_true(buf_chk(in_arr, BytesIO(), None, offset))
```

### Step 3: Assign in_arr = np.arange.reshape(...)

```python
in_arr = np.arange(24, dtype=dtype).reshape(shape)
```

**Verification:**
```python
assert_true(buf_chk(in_arr, out_buf, in_buf, offset))
```

### Step 4: Assign offset = 0

```python
offset = 0
```

**Verification:**
```python
assert_true(buf_chk(in_arr, out_buf, in_buf, offset))
```

### Step 5: Call assert_true()

```python
assert_true(buf_chk(in_arr, BytesIO(), None, offset))
```

**Verification:**
```python
assert_equal(len(arr), 0)
```

### Step 6: Assign offset = 10

```python
offset = 10
```

**Verification:**
```python
assert_equal(len(arr), 0)
```

### Step 7: Call assert_true()

```python
assert_true(buf_chk(in_arr, BytesIO(), None, offset))
```

**Verification:**
```python
assert_raises(IOError, array_from_file, shape, dtype, BytesIO())
```

### Step 8: Assign fname = 'test.bin'

```python
fname = 'test.bin'
```

**Verification:**
```python
assert_raises(Exception, array_from_file, shape, dtype, in_buf)
```

### Step 9: Assign arr = array_from_file(...)

```python
arr = array_from_file((), np.dtype('f8'), BytesIO())
```

### Step 10: Call assert_equal()

```python
assert_equal(len(arr), 0)
```

### Step 11: Assign arr = array_from_file(...)

```python
arr = array_from_file((0,), np.dtype('f8'), BytesIO())
```

### Step 12: Call assert_equal()

```python
assert_equal(len(arr), 0)
```

### Step 13: Call assert_raises()

```python
assert_raises(IOError, array_from_file, shape, dtype, BytesIO())
```

### Step 14: Assign unknown = tempfile.mkstemp(...)

```python
fd, fname = tempfile.mkstemp()
```

### Step 15: Assign out_buf = open(...)

```python
out_buf = open(fname, 'wb')
```

### Step 16: Assign in_buf = open(...)

```python
in_buf = open(fname, 'rb')
```

### Step 17: Call assert_true()

```python
assert_true(buf_chk(in_arr, out_buf, in_buf, offset))
```

### Step 18: Call out_buf.seek()

```python
out_buf.seek(0)
```

### Step 19: Call in_buf.seek()

```python
in_buf.seek(0)
```

### Step 20: Assign offset = 5

```python
offset = 5
```

### Step 21: Call assert_true()

```python
assert_true(buf_chk(in_arr, out_buf, in_buf, offset))
```

### Step 22: Call open.write()

```python
open(fname, 'wb').write(asbytes('1'))
```

### Step 23: Assign in_buf = open(...)

```python
in_buf = open(fname, 'rb')
```

### Step 24: Call assert_raises()

```python
assert_raises(Exception, array_from_file, shape, dtype, in_buf)
```


## Complete Example

```python
# Workflow
shape = (2, 3, 4)
dtype = np.dtype(np.float32)
in_arr = np.arange(24, dtype=dtype).reshape(shape)
offset = 0
assert_true(buf_chk(in_arr, BytesIO(), None, offset))
offset = 10
assert_true(buf_chk(in_arr, BytesIO(), None, offset))
fname = 'test.bin'
with InTemporaryDirectory():
    out_buf = open(fname, 'wb')
    in_buf = open(fname, 'rb')
    assert_true(buf_chk(in_arr, out_buf, in_buf, offset))
    out_buf.seek(0)
    in_buf.seek(0)
    offset = 5
    assert_true(buf_chk(in_arr, out_buf, in_buf, offset))
    del out_buf, in_buf
arr = array_from_file((), np.dtype('f8'), BytesIO())
assert_equal(len(arr), 0)
arr = array_from_file((0,), np.dtype('f8'), BytesIO())
assert_equal(len(arr), 0)
assert_raises(IOError, array_from_file, shape, dtype, BytesIO())
fd, fname = tempfile.mkstemp()
with InTemporaryDirectory():
    open(fname, 'wb').write(asbytes('1'))
    in_buf = open(fname, 'rb')
    assert_raises(Exception, array_from_file, shape, dtype, in_buf)
    del in_buf
```

## Next Steps


---

*Source: test_utils.py:51 | Complexity: Advanced | Last updated: 2026-05-18*