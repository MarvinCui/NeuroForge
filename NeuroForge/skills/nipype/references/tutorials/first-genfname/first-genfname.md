# How To: First Genfname

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test first genfname

## Prerequisites

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `nipype.utils.filemanip`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `nipype.interfaces.fsl`
- `nibabel`
- `numpy`
- `os.path`


## Step-by-Step Guide

### Step 1: Assign first = fsl.FIRST(...)

```python
first = fsl.FIRST()
```

**Verification:**
```python
assert value == expected_value
```

### Step 2: Assign first.inputs.out_file = 'segment.nii'

```python
first.inputs.out_file = 'segment.nii'
```

**Verification:**
```python
assert value == expected_value
```

### Step 3: Assign first.inputs.output_type = 'NIFTI_GZ'

```python
first.inputs.output_type = 'NIFTI_GZ'
```

**Verification:**
```python
assert value == expected_value
```

### Step 4: Assign value = first._gen_fname(...)

```python
value = first._gen_fname(basename='original_segmentations')
```

### Step 5: Assign expected_value = os.path.abspath(...)

```python
expected_value = os.path.abspath('segment_all_fast_origsegs.nii.gz')
```

**Verification:**
```python
assert value == expected_value
```

### Step 6: Assign first.inputs.method = 'none'

```python
first.inputs.method = 'none'
```

### Step 7: Assign value = first._gen_fname(...)

```python
value = first._gen_fname(basename='original_segmentations')
```

### Step 8: Assign expected_value = os.path.abspath(...)

```python
expected_value = os.path.abspath('segment_all_none_origsegs.nii.gz')
```

**Verification:**
```python
assert value == expected_value
```

### Step 9: Assign first.inputs.method = 'auto'

```python
first.inputs.method = 'auto'
```

### Step 10: Assign first.inputs.list_of_specific_structures = value

```python
first.inputs.list_of_specific_structures = ['L_Hipp', 'R_Hipp']
```

### Step 11: Assign value = first._gen_fname(...)

```python
value = first._gen_fname(basename='original_segmentations')
```

### Step 12: Assign expected_value = os.path.abspath(...)

```python
expected_value = os.path.abspath('segment_all_none_origsegs.nii.gz')
```

**Verification:**
```python
assert value == expected_value
```


## Complete Example

```python
# Workflow
first = fsl.FIRST()
first.inputs.out_file = 'segment.nii'
first.inputs.output_type = 'NIFTI_GZ'
value = first._gen_fname(basename='original_segmentations')
expected_value = os.path.abspath('segment_all_fast_origsegs.nii.gz')
assert value == expected_value
first.inputs.method = 'none'
value = first._gen_fname(basename='original_segmentations')
expected_value = os.path.abspath('segment_all_none_origsegs.nii.gz')
assert value == expected_value
first.inputs.method = 'auto'
first.inputs.list_of_specific_structures = ['L_Hipp', 'R_Hipp']
value = first._gen_fname(basename='original_segmentations')
expected_value = os.path.abspath('segment_all_none_origsegs.nii.gz')
assert value == expected_value
```

## Next Steps


---

*Source: test_preprocess.py:644 | Complexity: Advanced | Last updated: 2026-05-18*