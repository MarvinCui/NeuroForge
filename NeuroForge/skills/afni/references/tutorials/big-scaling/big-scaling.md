# How To: Big Scaling

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test big scaling

## Prerequisites

**Required Modules:**
- `numpy`
- `py3k`
- `numpy.testing`
- `spm99analyze`
- `casting`
- `testing`
- `scipy`
- `scipy.io`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert_true(np.allclose(data, data_back))
```

### Step 2: Call hdr.set_data_shape()

```python
hdr.set_data_shape((1, 1, 1))
```

### Step 3: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.int16)
```

### Step 4: Assign sio = BytesIO(...)

```python
sio = BytesIO()
```

### Step 5: Assign dtt = value

```python
dtt = np.float32
```

### Step 6: Assign data = value

```python
data = np.array([type_info(dtt)['max']], dtype=dtt)[:, None, None]
```

### Step 7: Call hdr.data_to_fileobj()

```python
hdr.data_to_fileobj(data, sio)
```

### Step 8: Assign data_back = hdr.data_from_fileobj(...)

```python
data_back = hdr.data_from_fileobj(sio)
```

### Step 9: Call assert_true()

```python
assert_true(np.allclose(data, data_back))
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
hdr.set_data_shape((1, 1, 1))
hdr.set_data_dtype(np.int16)
sio = BytesIO()
dtt = np.float32
data = np.array([type_info(dtt)['max']], dtype=dtt)[:, None, None]
hdr.data_to_fileobj(data, sio)
data_back = hdr.data_from_fileobj(sio)
assert_true(np.allclose(data, data_back))
```

## Next Steps


---

*Source: test_spm99analyze.py:57 | Complexity: Advanced | Last updated: 2026-05-18*