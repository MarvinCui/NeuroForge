# How To: Seg Filllesions

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test seg filllesions

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign seg_fill = FillLesions(...)

```python
seg_fill = FillLesions()
```

**Verification:**
```python
assert seg_fill.cmd == cmd
```

### Step 2: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_FillLesions', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert seg_fill.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 4: Assign lesion_mask = example_data(...)

```python
lesion_mask = example_data('im2.nii')
```

### Step 5: Assign seg_fill.inputs.in_file = in_file

```python
seg_fill.inputs.in_file = in_file
```

### Step 6: Assign seg_fill.inputs.lesion_mask = lesion_mask

```python
seg_fill.inputs.lesion_mask = lesion_mask
```

### Step 7: Assign expected_cmd = unknown.format(...)

```python
expected_cmd = '{cmd} -i {in_file} -l {lesion_mask} -o {out_file}'.format(cmd=cmd, in_file=in_file, lesion_mask=lesion_mask, out_file='im1_lesions_filled.nii.gz')
```

**Verification:**
```python
assert seg_fill.cmdline == expected_cmd
```

### Step 8: Call seg_fill.run()

```python
seg_fill.run()
```


## Complete Example

```python
# Workflow
seg_fill = FillLesions()
cmd = get_custom_path('seg_FillLesions', env_dir='NIFTYSEGDIR')
assert seg_fill.cmd == cmd
with pytest.raises(ValueError):
    seg_fill.run()
in_file = example_data('im1.nii')
lesion_mask = example_data('im2.nii')
seg_fill.inputs.in_file = in_file
seg_fill.inputs.lesion_mask = lesion_mask
expected_cmd = '{cmd} -i {in_file} -l {lesion_mask} -o {out_file}'.format(cmd=cmd, in_file=in_file, lesion_mask=lesion_mask, out_file='im1_lesions_filled.nii.gz')
assert seg_fill.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_lesions.py:15 | Complexity: Advanced | Last updated: 2026-05-18*