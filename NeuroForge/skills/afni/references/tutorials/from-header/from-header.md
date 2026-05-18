# How To: From Header

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test from header

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `logging`
- `pickle`
- `numpy`
- `py3k`
- `volumeutils`
- `spatialimages`
- `analyze`
- `nifti1`
- `loadsave`
- `casting`
- `numpy.testing`
- `testing`
- `test_wrapstruct`


## Step-by-Step Guide

### Step 1: Assign klass = value

```python
klass = self.header_class
```

**Verification:**
```python
assert_equal(klass(), empty)
```

### Step 2: Assign empty = klass.from_header(...)

```python
empty = klass.from_header()
```

**Verification:**
```python
assert_equal(klass(), empty)
```

### Step 3: Call assert_equal()

```python
assert_equal(klass(), empty)
```

**Verification:**
```python
assert_equal(hdr, copy)
```

### Step 4: Assign empty = klass.from_header(...)

```python
empty = klass.from_header(None)
```

**Verification:**
```python
assert_false(hdr is copy)
```

### Step 5: Call assert_equal()

```python
assert_equal(klass(), empty)
```

**Verification:**
```python
assert_true(isinstance(converted, klass))
```

### Step 6: Assign hdr = klass(...)

```python
hdr = klass()
```

**Verification:**
```python
assert_equal(converted.get_data_dtype(), np.dtype('i2'))
```

### Step 7: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.float64)
```

**Verification:**
```python
assert_equal(converted.get_data_shape(), (5, 4, 3))
```

### Step 8: Call hdr.set_data_shape()

```python
hdr.set_data_shape((1, 2, 3))
```

**Verification:**
```python
assert_equal(converted.get_zooms(), (10.0, 9.0, 8.0))
```

### Step 9: Call hdr.set_zooms()

```python
hdr.set_zooms((3.0, 2.0, 1.0))
```

### Step 10: Assign copy = klass.from_header(...)

```python
copy = klass.from_header(hdr)
```

### Step 11: Call assert_equal()

```python
assert_equal(hdr, copy)
```

### Step 12: Call assert_false()

```python
assert_false(hdr is copy)
```

### Step 13: Assign converted = klass.from_header(...)

```python
converted = klass.from_header(C())
```

### Step 14: Call assert_true()

```python
assert_true(isinstance(converted, klass))
```

### Step 15: Call assert_equal()

```python
assert_equal(converted.get_data_dtype(), np.dtype('i2'))
```

### Step 16: Call assert_equal()

```python
assert_equal(converted.get_data_shape(), (5, 4, 3))
```

### Step 17: Call assert_equal()

```python
assert_equal(converted.get_zooms(), (10.0, 9.0, 8.0))
```


## Complete Example

```python
# Workflow
klass = self.header_class
empty = klass.from_header()
assert_equal(klass(), empty)
empty = klass.from_header(None)
assert_equal(klass(), empty)
hdr = klass()
hdr.set_data_dtype(np.float64)
hdr.set_data_shape((1, 2, 3))
hdr.set_zooms((3.0, 2.0, 1.0))
copy = klass.from_header(hdr)
assert_equal(hdr, copy)
assert_false(hdr is copy)

class C(object):

    def get_data_dtype(self):
        return np.dtype('i2')

    def get_data_shape(self):
        return (5, 4, 3)

    def get_zooms(self):
        return (10.0, 9.0, 8.0)
converted = klass.from_header(C())
assert_true(isinstance(converted, klass))
assert_equal(converted.get_data_dtype(), np.dtype('i2'))
assert_equal(converted.get_data_shape(), (5, 4, 3))
assert_equal(converted.get_zooms(), (10.0, 9.0, 8.0))
```

## Next Steps


---

*Source: test_analyze.py:416 | Complexity: Advanced | Last updated: 2026-05-18*