# How To: Validate File Stream Equivalence

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: validate file stream equivalence

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `pathlib`
- `sys`
- `warnings`
- `functools`
- `itertools`
- `numpy`
- `optpkg`
- `unittest`
- `pytest`
- `numpy.testing`
- `nibabel.arraywriters`
- `nibabel.testing`
- `casting`
- `spatialimages`
- `tmpdirs`
- `test_api_validators`
- `test_brikhead`
- `test_minc1`
- `test_minc2`
- `test_parrec`
- `uuid`

**Setup Required:**
```python
# Fixtures: imaker, params
```

## Step-by-Step Guide

### Step 1: Assign img = imaker(...)

```python
img = imaker()
```

**Verification:**
```python
assert contents1 == contents2
```

### Step 2: Assign klass = getattr(...)

```python
klass = getattr(self, 'klass', img.__class__)
```

**Verification:**
```python
assert np.array_equal(img_a.get_fdata(), img_b.get_fdata())
```

### Step 3: Assign fname = value

```python
fname = 'img' + self.standard_extension
```

**Verification:**
```python
assert self._header_eq(img_a.header, img_b.header)
```

### Step 4: Call img.to_filename()

```python
img.to_filename(fname)
```

### Step 5: Assign contents1 = pathlib.Path.read_bytes(...)

```python
contents1 = pathlib.Path(fname).read_bytes()
```

### Step 6: Assign contents2 = pathlib.Path.read_bytes(...)

```python
contents2 = pathlib.Path('stream').read_bytes()
```

**Verification:**
```python
assert contents1 == contents2
```

### Step 7: Assign img_a = klass.from_filename(...)

```python
img_a = klass.from_filename(fname)
```

**Verification:**
```python
assert self._header_eq(img_a.header, img_b.header)
```

### Step 8: Call img.to_stream()

```python
img.to_stream(fobj)
```

### Step 9: Assign img_b = klass.from_stream(...)

```python
img_b = klass.from_stream(fobj)
```

**Verification:**
```python
assert np.array_equal(img_a.get_fdata(), img_b.get_fdata())
```


## Complete Example

```python
# Setup
# Fixtures: imaker, params

# Workflow
img = imaker()
klass = getattr(self, 'klass', img.__class__)
with InTemporaryDirectory():
    fname = 'img' + self.standard_extension
    img.to_filename(fname)
    with open('stream', 'wb') as fobj:
        img.to_stream(fobj)
    contents1 = pathlib.Path(fname).read_bytes()
    contents2 = pathlib.Path('stream').read_bytes()
    assert contents1 == contents2
    img_a = klass.from_filename(fname)
    with open(fname, 'rb') as fobj:
        img_b = klass.from_stream(fobj)
        assert np.array_equal(img_a.get_fdata(), img_b.get_fdata())
    assert self._header_eq(img_a.header, img_b.header)
    del img_a
    del img_b
```

## Next Steps


---

*Source: test_image_api.py:502 | Complexity: Advanced | Last updated: 2026-05-18*