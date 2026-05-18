# How To: Type Info

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test type info

## Prerequisites

**Required Modules:**
- `numpy`
- `casting`
- `nose`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign info = np.finfo(...)

```python
info = np.finfo(np.longdouble)
```

**Verification:**
```python
assert_equal(dict(min=info.min, max=info.max, nexp=None, nmant=None, minexp=None, maxexp=None, width=np.dtype(dtt).itemsize), infod)
```

### Step 2: Assign dbl_info = np.finfo(...)

```python
dbl_info = np.finfo(np.float64)
```

**Verification:**
```python
assert_equal(infod['min'].dtype.type, dtt)
```

### Step 3: Assign infod = type_info(...)

```python
infod = type_info(np.longdouble)
```

**Verification:**
```python
assert_equal(infod['max'].dtype.type, dtt)
```

### Step 4: Assign width = value

```python
width = np.dtype(np.longdouble).itemsize
```

**Verification:**
```python
assert_equal(dict(min=info.min, max=info.max, nexp=info.nexp, nmant=info.nmant, minexp=info.minexp, maxexp=info.maxexp, width=np.dtype(dtt).itemsize), infod)
```

### Step 5: Assign vals = value

```python
vals = (info.nmant, info.nexp, width)
```

**Verification:**
```python
assert_equal(infod['min'].dtype.type, dtt)
```

### Step 6: Assign info = np.iinfo(...)

```python
info = np.iinfo(dtt)
```

**Verification:**
```python
assert_equal(infod['max'].dtype.type, dtt)
```

### Step 7: Assign infod = type_info(...)

```python
infod = type_info(dtt)
```

**Verification:**
```python
assert_equal(dict(min=info.min, max=info.max, minexp=info.minexp, maxexp=info.maxexp, nexp=info.nexp, nmant=info.nmant, width=width), infod)
```

### Step 8: Call assert_equal()

```python
assert_equal(dict(min=info.min, max=info.max, nexp=None, nmant=None, minexp=None, maxexp=None, width=np.dtype(dtt).itemsize), infod)
```

**Verification:**
```python
assert_equal(dict(min=dbl_info.min, max=dbl_info.max, minexp=-1022, maxexp=1024, nexp=11, nmant=106, width=16), infod)
```

### Step 9: Call assert_equal()

```python
assert_equal(infod['min'].dtype.type, dtt)
```

**Verification:**
```python
assert_equal(exp_res, infod)
```

### Step 10: Call assert_equal()

```python
assert_equal(infod['max'].dtype.type, dtt)
```

### Step 11: Assign info = np.finfo(...)

```python
info = np.finfo(dtt)
```

### Step 12: Assign infod = type_info(...)

```python
infod = type_info(dtt)
```

### Step 13: Call assert_equal()

```python
assert_equal(dict(min=info.min, max=info.max, nexp=info.nexp, nmant=info.nmant, minexp=info.minexp, maxexp=info.maxexp, width=np.dtype(dtt).itemsize), infod)
```

### Step 14: Call assert_equal()

```python
assert_equal(infod['min'].dtype.type, dtt)
```

### Step 15: Call assert_equal()

```python
assert_equal(infod['max'].dtype.type, dtt)
```

### Step 16: Call assert_equal()

```python
assert_equal(dict(min=info.min, max=info.max, minexp=info.minexp, maxexp=info.maxexp, nexp=info.nexp, nmant=info.nmant, width=width), infod)
```

### Step 17: Call assert_equal()

```python
assert_equal(dict(min=dbl_info.min, max=dbl_info.max, minexp=-1022, maxexp=1024, nexp=11, nmant=106, width=16), infod)
```

### Step 18: Assign exp_res = type_info(...)

```python
exp_res = type_info(np.float64)
```

### Step 19: Assign unknown = width

```python
exp_res['width'] = width
```

### Step 20: Call assert_equal()

```python
assert_equal(exp_res, infod)
```


## Complete Example

```python
# Workflow
for dtt in np.sctypes['int'] + np.sctypes['uint']:
    info = np.iinfo(dtt)
    infod = type_info(dtt)
    assert_equal(dict(min=info.min, max=info.max, nexp=None, nmant=None, minexp=None, maxexp=None, width=np.dtype(dtt).itemsize), infod)
    assert_equal(infod['min'].dtype.type, dtt)
    assert_equal(infod['max'].dtype.type, dtt)
for dtt in IEEE_floats + [np.complex64, np.complex64]:
    info = np.finfo(dtt)
    infod = type_info(dtt)
    assert_equal(dict(min=info.min, max=info.max, nexp=info.nexp, nmant=info.nmant, minexp=info.minexp, maxexp=info.maxexp, width=np.dtype(dtt).itemsize), infod)
    assert_equal(infod['min'].dtype.type, dtt)
    assert_equal(infod['max'].dtype.type, dtt)
info = np.finfo(np.longdouble)
dbl_info = np.finfo(np.float64)
infod = type_info(np.longdouble)
width = np.dtype(np.longdouble).itemsize
vals = (info.nmant, info.nexp, width)
if vals in ((52, 11, 8), (63, 15, 12), (63, 15, 16), (112, 15, 16), (106, 11, 16)):
    assert_equal(dict(min=info.min, max=info.max, minexp=info.minexp, maxexp=info.maxexp, nexp=info.nexp, nmant=info.nmant, width=width), infod)
elif vals == (1, 1, 16):
    assert_equal(dict(min=dbl_info.min, max=dbl_info.max, minexp=-1022, maxexp=1024, nexp=11, nmant=106, width=16), infod)
elif vals == (52, 15, 12):
    exp_res = type_info(np.float64)
    exp_res['width'] = width
    assert_equal(exp_res, infod)
else:
    raise ValueError('Unexpected float type to test')
```

## Next Steps


---

*Source: test_floating.py:25 | Complexity: Advanced | Last updated: 2026-05-18*