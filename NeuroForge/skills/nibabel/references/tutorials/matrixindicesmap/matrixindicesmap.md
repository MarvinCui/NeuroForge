# How To: Matrixindicesmap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test matrixindicesmap

## Prerequisites

**Required Modules:**
- `collections`
- `xml.etree`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.cifti2.cifti2`
- `nibabel.nifti2`
- `nibabel.tests.test_dataobj_images`
- `nibabel.tests.test_image_api`


## Step-by-Step Guide

### Step 1: Assign mim = ci.Cifti2MatrixIndicesMap(...)

```python
mim = ci.Cifti2MatrixIndicesMap(0, 'CIFTI_INDEX_TYPE_LABELS')
```

**Verification:**
```python
assert mim.volume is None
```

### Step 2: Assign volume = ci.Cifti2Volume(...)

```python
volume = ci.Cifti2Volume()
```

**Verification:**
```python
assert mim.volume == volume
```

### Step 3: Assign volume2 = ci.Cifti2Volume(...)

```python
volume2 = ci.Cifti2Volume()
```

**Verification:**
```python
assert mim.volume == volume2
```

### Step 4: Assign parcel = ci.Cifti2Parcel(...)

```python
parcel = ci.Cifti2Parcel()
```

**Verification:**
```python
assert mim.volume is None
```

### Step 5: Call mim.extend()

```python
mim.extend((volume, parcel))
```

**Verification:**
```python
assert mim.volume == volume
```

### Step 6: Assign unknown = volume2

```python
mim[0] = volume2
```

**Verification:**
```python
assert mim.volume == volume2
```

### Step 7: Assign mim.volume = volume

```python
mim.volume = volume
```

**Verification:**
```python
assert mim.volume == volume
```

### Step 8: Assign mim.volume = volume2

```python
mim.volume = volume2
```

**Verification:**
```python
assert mim.volume == volume2
```

### Step 9: Call mim.insert()

```python
mim.insert(0, volume)
```

### Step 10: Assign unknown = volume

```python
mim[1] = volume
```

### Step 11: Assign mim.volume = parcel

```python
mim.volume = parcel
```


## Complete Example

```python
# Workflow
mim = ci.Cifti2MatrixIndicesMap(0, 'CIFTI_INDEX_TYPE_LABELS')
volume = ci.Cifti2Volume()
volume2 = ci.Cifti2Volume()
parcel = ci.Cifti2Parcel()
assert mim.volume is None
mim.extend((volume, parcel))
assert mim.volume == volume
with pytest.raises(ci.Cifti2HeaderError):
    mim.insert(0, volume)
with pytest.raises(ci.Cifti2HeaderError):
    mim[1] = volume
mim[0] = volume2
assert mim.volume == volume2
del mim.volume
assert mim.volume is None
with pytest.raises(ValueError):
    del mim.volume
mim.volume = volume
assert mim.volume == volume
mim.volume = volume2
assert mim.volume == volume2
with pytest.raises(ValueError):
    mim.volume = parcel
```

## Next Steps


---

*Source: test_cifti2.py:326 | Complexity: Advanced | Last updated: 2026-05-18*