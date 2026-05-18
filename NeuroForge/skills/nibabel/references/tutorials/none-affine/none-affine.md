# How To: None Affine

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test none affine

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

### Step 1: Assign img_klass = value

```python
img_klass = self.image_class
```

**Verification:**
```python
assert_array_equal(img_back.affine, aff)
```

### Step 2: Assign img = img_klass(...)

```python
img = img_klass(np.zeros((2, 3, 4)), None)
```

### Step 3: Assign aff = img.header.get_best_affine(...)

```python
aff = img.header.get_best_affine()
```

### Step 4: Call img.to_file_map()

```python
img.to_file_map()
```

### Step 5: Assign img_back = img.from_file_map(...)

```python
img_back = img.from_file_map(img.file_map)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(img_back.affine, aff)
```

### Step 7: Assign value.fileobj = BytesIO(...)

```python
value.fileobj = BytesIO()
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
img = img_klass(np.zeros((2, 3, 4)), None)
aff = img.header.get_best_affine()
for value in img.file_map.values():
    value.fileobj = BytesIO()
img.to_file_map()
img_back = img.from_file_map(img.file_map)
assert_array_equal(img_back.affine, aff)
```

## Next Steps


---

*Source: test_spm99analyze.py:470 | Complexity: Intermediate | Last updated: 2026-05-18*