# How To: Data Array Round Trip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test data array round trip

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.tmpdirs`
- `fileholders`
- `nifti1`
- `testing`
- `test_parse_gifti_fast`
- `gifti`


## Step-by-Step Guide

### Step 1: Assign verts = np.zeros(...)

```python
verts = np.zeros((4, 3), np.float32)
```

**Verification:**
```python
assert_array_equal(vertices, verts)
```

### Step 2: Assign unknown = 10.5

```python
verts[0, 0] = 10.5
```

### Step 3: Assign unknown = 20.5

```python
verts[1, 1] = 20.5
```

### Step 4: Assign unknown = 30.5

```python
verts[2, 2] = 30.5
```

### Step 5: Assign vertices = GiftiDataArray(...)

```python
vertices = GiftiDataArray(verts)
```

### Step 6: Assign img = GiftiImage(...)

```python
img = GiftiImage()
```

### Step 7: Call img.add_gifti_data_array()

```python
img.add_gifti_data_array(vertices)
```

### Step 8: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

### Step 9: Assign fmap = dict(...)

```python
fmap = dict(image=FileHolder(fileobj=bio))
```

### Step 10: Call bio.write()

```python
bio.write(img.to_xml())
```

### Step 11: Call bio.seek()

```python
bio.seek(0)
```

### Step 12: Assign gio = GiftiImage.from_file_map(...)

```python
gio = GiftiImage.from_file_map(fmap)
```

### Step 13: Assign vertices = value

```python
vertices = gio.darrays[0].data
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(vertices, verts)
```


## Complete Example

```python
# Workflow
verts = np.zeros((4, 3), np.float32)
verts[0, 0] = 10.5
verts[1, 1] = 20.5
verts[2, 2] = 30.5
vertices = GiftiDataArray(verts)
img = GiftiImage()
img.add_gifti_data_array(vertices)
bio = BytesIO()
fmap = dict(image=FileHolder(fileobj=bio))
bio.write(img.to_xml())
bio.seek(0)
gio = GiftiImage.from_file_map(fmap)
vertices = gio.darrays[0].data
assert_array_equal(vertices, verts)
```

## Next Steps


---

*Source: test_gifti.py:528 | Complexity: Advanced | Last updated: 2026-05-18*