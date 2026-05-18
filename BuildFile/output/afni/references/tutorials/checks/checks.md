# How To: Checks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test checks

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

### Step 1: Assign hdr_t = self.header_class(...)

```python
hdr_t = self.header_class()
```

**Verification:**
```python
assert_equal(self._dxer(hdr_t), '')
```

### Step 2: Call assert_equal()

```python
assert_equal(self._dxer(hdr_t), '')
```

**Verification:**
```python
assert_equal(self._dxer(hdr), 'sizeof_hdr should be 348')
```

### Step 3: Assign hdr = hdr_t.copy(...)

```python
hdr = hdr_t.copy()
```

**Verification:**
```python
assert_equal(self._dxer(hdr), 'data code 0 not supported\nbitpix does not match datatype')
```

### Step 4: Assign unknown = 1

```python
hdr['sizeof_hdr'] = 1
```

**Verification:**
```python
assert_equal(self._dxer(hdr), 'bitpix does not match datatype')
```

### Step 5: Call assert_equal()

```python
assert_equal(self._dxer(hdr), 'sizeof_hdr should be 348')
```

**Verification:**
```python
assert_equal(self._dxer(hdr), 'pixdim[1,2,3] should be positive')
```

### Step 6: Assign hdr = hdr_t.copy(...)

```python
hdr = hdr_t.copy()
```

### Step 7: Assign unknown = 0

```python
hdr['datatype'] = 0
```

### Step 8: Call assert_equal()

```python
assert_equal(self._dxer(hdr), 'data code 0 not supported\nbitpix does not match datatype')
```

### Step 9: Assign hdr = hdr_t.copy(...)

```python
hdr = hdr_t.copy()
```

### Step 10: Assign unknown = 0

```python
hdr['bitpix'] = 0
```

### Step 11: Call assert_equal()

```python
assert_equal(self._dxer(hdr), 'bitpix does not match datatype')
```

### Step 12: Assign hdr = hdr_t.copy(...)

```python
hdr = hdr_t.copy()
```

### Step 13: Assign unknown = value

```python
hdr['pixdim'][i] = -1
```

### Step 14: Call assert_equal()

```python
assert_equal(self._dxer(hdr), 'pixdim[1,2,3] should be positive')
```


## Complete Example

```python
# Workflow
hdr_t = self.header_class()
assert_equal(self._dxer(hdr_t), '')
hdr = hdr_t.copy()
hdr['sizeof_hdr'] = 1
assert_equal(self._dxer(hdr), 'sizeof_hdr should be 348')
hdr = hdr_t.copy()
hdr['datatype'] = 0
assert_equal(self._dxer(hdr), 'data code 0 not supported\nbitpix does not match datatype')
hdr = hdr_t.copy()
hdr['bitpix'] = 0
assert_equal(self._dxer(hdr), 'bitpix does not match datatype')
for i in (1, 2, 3):
    hdr = hdr_t.copy()
    hdr['pixdim'][i] = -1
    assert_equal(self._dxer(hdr), 'pixdim[1,2,3] should be positive')
```

## Next Steps


---

*Source: test_analyze.py:88 | Complexity: Advanced | Last updated: 2026-05-18*