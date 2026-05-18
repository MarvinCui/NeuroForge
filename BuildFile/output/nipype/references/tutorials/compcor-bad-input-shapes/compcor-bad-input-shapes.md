# How To: Compcor Bad Input Shapes

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test compcor bad input shapes

## Prerequisites

**Required Modules:**
- `os`
- `nibabel`
- `numpy`
- `pytest`
- `testing`
- `confounds`


## Step-by-Step Guide

### Step 1: Assign shape_less_than = value

```python
shape_less_than = (1, 2, 2, 5)
```

### Step 2: Assign shape_more_than = value

```python
shape_more_than = (3, 3, 3, 5)
```

### Step 3: Assign data_file = utils.save_toy_nii(...)

```python
data_file = utils.save_toy_nii(np.zeros(data_shape), 'temp.nii')
```

### Step 4: Assign interface = CompCor(...)

```python
interface = CompCor(realigned_file=data_file, mask_files=self.mask_files[0])
```

### Step 5: Call interface.run()

```python
interface.run()
```


## Complete Example

```python
# Workflow
shape_less_than = (1, 2, 2, 5)
shape_more_than = (3, 3, 3, 5)
for data_shape in (shape_less_than, shape_more_than):
    data_file = utils.save_toy_nii(np.zeros(data_shape), 'temp.nii')
    interface = CompCor(realigned_file=data_file, mask_files=self.mask_files[0])
    with pytest.raises(ValueError):
        interface.run()
```

## Next Steps


---

*Source: test_CompCor.py:195 | Complexity: Intermediate | Last updated: 2026-05-18*