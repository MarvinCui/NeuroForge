# How To: Read Ones

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test read ones

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `numpy`
- `nibabel`
- `nibabel.cifti2`
- `nibabel.tests.nibabel_data`


## Step-by-Step Guide

### Step 1: Assign img = nib.load(...)

```python
img = nib.load(os.path.join(test_directory, 'ones.dscalar.nii'))
```

**Verification:**
```python
assert (arr == 1).all()
```

### Step 2: Assign arr = img.get_fdata(...)

```python
arr = img.get_fdata()
```

**Verification:**
```python
assert isinstance(axes[0], cifti2_axes.ScalarAxis)
```

### Step 3: Assign axes = value

```python
axes = [img.header.get_axis(dim) for dim in range(2)]
```

**Verification:**
```python
assert len(axes[0]) == 1
```

### Step 4: Call check_hcp_grayordinates()

```python
check_hcp_grayordinates(axes[1])
```

**Verification:**
```python
assert axes[0].name[0] == 'ones'
```

### Step 5: Assign img = check_rewrite(...)

```python
img = check_rewrite(arr, axes)
```

**Verification:**
```python
assert axes[0].meta[0] == {}
```

### Step 6: Call check_hcp_grayordinates()

```python
check_hcp_grayordinates(img.header.get_axis(1))
```


## Complete Example

```python
# Workflow
img = nib.load(os.path.join(test_directory, 'ones.dscalar.nii'))
arr = img.get_fdata()
axes = [img.header.get_axis(dim) for dim in range(2)]
assert (arr == 1).all()
assert isinstance(axes[0], cifti2_axes.ScalarAxis)
assert len(axes[0]) == 1
assert axes[0].name[0] == 'ones'
assert axes[0].meta[0] == {}
check_hcp_grayordinates(axes[1])
img = check_rewrite(arr, axes)
check_hcp_grayordinates(img.header.get_axis(1))
```

## Next Steps


---

*Source: test_cifti2io_axes.py:145 | Complexity: Intermediate | Last updated: 2026-05-18*