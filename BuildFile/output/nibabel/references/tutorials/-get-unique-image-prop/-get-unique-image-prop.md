# How To:  Get Unique Image Prop

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test  get unique image prop

## Prerequisites

**Required Modules:**
- `glob`
- `os.path`
- `os.path`
- `warnings`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `fileholders`
- `nifti1`
- `openers`
- `parrec`
- `testing`
- `volumeutils`
- `test_arrayproxy`


## Step-by-Step Guide

### Step 1: Assign hdr = PARRECHeader(...)

```python
hdr = PARRECHeader(HDR_INFO, HDR_DEFS.copy())
```

**Verification:**
```python
assert uip('image pixel size') == 16
```

### Step 2: Assign uip = value

```python
uip = hdr._get_unique_image_prop
```

**Verification:**
```python
assert_array_equal(uip('recon resolution'), [64, 64])
```

### Step 3: Assign unknown = 32

```python
hdr.image_defs['image pixel size'][3] = 32
```

**Verification:**
```python
assert_array_equal(uip('image angulation'), [-13.26, 0, 0])
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(uip('recon resolution'), [64, 64])
```

### Step 5: Assign unknown = 32

```python
hdr.image_defs['recon resolution'][4, 1] = 32
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(uip('image angulation'), [-13.26, 0, 0])
```

### Step 7: Assign unknown = 1

```python
hdr.image_defs['image angulation'][5, 2] = 1
```

### Step 8: Call uip()

```python
uip('image pixel size')
```

### Step 9: Call uip()

```python
uip('recon resolution')
```

### Step 10: Call uip()

```python
uip('image angulation')
```

### Step 11: Call uip()

```python
uip('slice number')
```


## Complete Example

```python
# Workflow
hdr = PARRECHeader(HDR_INFO, HDR_DEFS.copy())
uip = hdr._get_unique_image_prop
assert uip('image pixel size') == 16
hdr.image_defs['image pixel size'][3] = 32
with pytest.raises(PARRECError):
    uip('image pixel size')
assert_array_equal(uip('recon resolution'), [64, 64])
hdr.image_defs['recon resolution'][4, 1] = 32
with pytest.raises(PARRECError):
    uip('recon resolution')
assert_array_equal(uip('image angulation'), [-13.26, 0, 0])
hdr.image_defs['image angulation'][5, 2] = 1
with pytest.raises(PARRECError):
    uip('image angulation')
with pytest.raises(PARRECError):
    uip('slice number')
```

## Next Steps


---

*Source: test_parrec.py:633 | Complexity: Advanced | Last updated: 2026-05-18*