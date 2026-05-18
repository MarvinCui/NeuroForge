# How To: Origin Checks

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test origin checks

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

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert_equal(fhdr, hdr)
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

**Verification:**
```python
assert_equal(message, 'very large origin values relative to dims; leaving as set, ignoring for affine')
```

### Step 3: Assign hdr.data_shape = value

```python
hdr.data_shape = [1, 1, 1]
```

**Verification:**
```python
assert_raises(*raiser)
```

### Step 4: Assign unknown = 101

```python
hdr['origin'][0] = 101
```

**Verification:**
```python
assert_equal(dxer(hdr.binaryblock), 'very large origin values relative to dims')
```

### Step 5: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 20)
```

### Step 6: Call assert_equal()

```python
assert_equal(fhdr, hdr)
```

### Step 7: Call assert_equal()

```python
assert_equal(message, 'very large origin values relative to dims; leaving as set, ignoring for affine')
```

### Step 8: Call assert_raises()

```python
assert_raises(*raiser)
```

### Step 9: Assign dxer = value

```python
dxer = self.header_class.diagnose_binaryblock
```

### Step 10: Call assert_equal()

```python
assert_equal(dxer(hdr.binaryblock), 'very large origin values relative to dims')
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
hdr.data_shape = [1, 1, 1]
hdr['origin'][0] = 101
fhdr, message, raiser = self.log_chk(hdr, 20)
assert_equal(fhdr, hdr)
assert_equal(message, 'very large origin values relative to dims; leaving as set, ignoring for affine')
assert_raises(*raiser)
dxer = self.header_class.diagnose_binaryblock
assert_equal(dxer(hdr.binaryblock), 'very large origin values relative to dims')
```

## Next Steps


---

*Source: test_spm99analyze.py:71 | Complexity: Advanced | Last updated: 2026-05-18*