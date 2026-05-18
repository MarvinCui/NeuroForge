# How To: Compressed

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test compressed

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `gzip`
- `bz2`
- `numpy`
- `externals.netcdf`
- `minc`
- `nose.tools`
- `numpy.testing`
- `tmpdirs`
- `testing`


## Step-by-Step Guide

### Step 1: Assign content = open.read(...)

```python
content = open(MINC_EXAMPLE['fname'], 'rb').read()
```

**Verification:**
```python
assert_array_almost_equal(data.mean(), 0.60602819)
```

### Step 2: Assign openers_exts = value

```python
openers_exts = ((gzip.open, '.gz'), (bz2.BZ2File, '.bz2'))
```

### Step 3: Assign fname = value

```python
fname = 'test.mnc' + ext
```

### Step 4: Assign fobj = opener(...)

```python
fobj = opener(fname, 'wb')
```

### Step 5: Call fobj.write()

```python
fobj.write(content)
```

### Step 6: Call fobj.close()

```python
fobj.close()
```

### Step 7: Assign img = load(...)

```python
img = load(fname)
```

### Step 8: Assign data = img.get_data(...)

```python
data = img.get_data()
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(data.mean(), 0.60602819)
```


## Complete Example

```python
# Workflow
content = open(MINC_EXAMPLE['fname'], 'rb').read()
openers_exts = ((gzip.open, '.gz'), (bz2.BZ2File, '.bz2'))
with InTemporaryDirectory():
    for opener, ext in openers_exts:
        fname = 'test.mnc' + ext
        fobj = opener(fname, 'wb')
        fobj.write(content)
        fobj.close()
        img = load(fname)
        data = img.get_data()
        assert_array_almost_equal(data.mean(), 0.60602819)
        del img
```

## Next Steps


---

*Source: test_minc.py:65 | Complexity: Advanced | Last updated: 2026-05-18*