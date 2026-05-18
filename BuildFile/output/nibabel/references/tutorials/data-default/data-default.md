# How To: Data Default

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test data default

## Prerequisites

**Required Modules:**
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `imageclasses`
- `spatialimages`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign img_klass = value

```python
img_klass = self.image_class
```

### Step 2: Assign hdr_klass = value

```python
hdr_klass = self.image_class.header_class
```

### Step 3: Assign data = np.arange.reshape(...)

```python
data = np.arange(24, dtype=np.int32).reshape((2, 3, 4))
```

### Step 4: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 5: Assign img = img_klass(...)

```python
img = img_klass(data, affine)
```

### Step 6: Call self.check_dtypes()

```python
self.check_dtypes(data.dtype, img.get_data_dtype())
```

### Step 7: Assign header = hdr_klass(...)

```python
header = hdr_klass()
```

### Step 8: Call header.set_data_dtype()

```python
header.set_data_dtype(np.float32)
```

### Step 9: Assign img = img_klass(...)

```python
img = img_klass(data, affine, header)
```

### Step 10: Call self.check_dtypes()

```python
self.check_dtypes(np.dtype(np.float32), img.get_data_dtype())
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
hdr_klass = self.image_class.header_class
data = np.arange(24, dtype=np.int32).reshape((2, 3, 4))
affine = np.eye(4)
img = img_klass(data, affine)
self.check_dtypes(data.dtype, img.get_data_dtype())
header = hdr_klass()
header.set_data_dtype(np.float32)
img = img_klass(data, affine, header)
self.check_dtypes(np.dtype(np.float32), img.get_data_dtype())
```

## Next Steps


---

*Source: test_spatialimages.py:261 | Complexity: Advanced | Last updated: 2026-05-18*