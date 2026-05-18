# How To: Origin Checks

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test origin checks

## Prerequisites

**Required Modules:**
- `itertools`
- `unittest`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `optpkg`
- `casting`
- `spatialimages`
- `spm99analyze`
- `testing`
- `volumeutils`
- `scipy.io`


## Step-by-Step Guide

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert fhdr == hdr
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

**Verification:**
```python
assert message == 'very large origin values relative to dims; leaving as set, ignoring for affine'
```

### Step 3: Assign hdr.data_shape = value

```python
hdr.data_shape = [1, 1, 1]
```

**Verification:**
```python
assert dxer(hdr.binaryblock) == 'very large origin values relative to dims'
```

### Step 4: Assign unknown = 101

```python
hdr['origin'][0] = 101
```

### Step 5: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 20)
```

**Verification:**
```python
assert fhdr == hdr
```

### Step 6: Call pytest.raises()

```python
pytest.raises(*raiser)
```

### Step 7: Assign dxer = value

```python
dxer = self.header_class.diagnose_binaryblock
```

**Verification:**
```python
assert dxer(hdr.binaryblock) == 'very large origin values relative to dims'
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
hdr.data_shape = [1, 1, 1]
hdr['origin'][0] = 101
fhdr, message, raiser = self.log_chk(hdr, 20)
assert fhdr == hdr
assert message == 'very large origin values relative to dims; leaving as set, ignoring for affine'
pytest.raises(*raiser)
dxer = self.header_class.diagnose_binaryblock
assert dxer(hdr.binaryblock) == 'very large origin values relative to dims'
```

## Next Steps


---

*Source: test_spm99analyze.py:149 | Complexity: Intermediate | Last updated: 2026-05-18*