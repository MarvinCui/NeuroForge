# How To: Tbss Skeleton

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test tbss skeleton

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `nipype.interfaces.fsl.dti`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `pytest`
- `nipype.testing.fixtures`

**Setup Required:**
```python
# Fixtures: create_files_in_directory
```

## Step-by-Step Guide

### Step 1: Assign skeletor = fsl.TractSkeleton(...)

```python
skeletor = fsl.TractSkeleton()
```

**Verification:**
```python
assert skeletor.cmd == 'tbss_skeleton'
```

### Step 2: Assign unknown = create_files_in_directory

```python
files, newdir = create_files_in_directory
```

**Verification:**
```python
assert skeletor.cmdline == 'tbss_skeleton -i a.nii -o %s' % os.path.join(newdir, 'a_skeleton.nii')
```

### Step 3: Assign skeletor.inputs.in_file = value

```python
skeletor.inputs.in_file = files[0]
```

**Verification:**
```python
assert skeletor.cmdline == 'tbss_skeleton -i a.nii -o old_boney.nii'
```

### Step 4: Assign skeletor.inputs.skeleton_file = True

```python
skeletor.inputs.skeleton_file = True
```

**Verification:**
```python
assert bones.cmdline == 'tbss_skeleton -i a.nii -p 0.200 b.nii {} b.nii {}'.format(Info.standard_image('LowerCingulum_1mm.nii.gz'), os.path.join(newdir, 'b_skeletonised.nii'))
```

### Step 5: Assign skeletor.inputs.skeleton_file = 'old_boney.nii'

```python
skeletor.inputs.skeleton_file = 'old_boney.nii'
```

**Verification:**
```python
assert bones.cmdline == 'tbss_skeleton -i a.nii -p 0.200 b.nii a.nii b.nii %s' % os.path.join(newdir, 'b_skeletonised.nii')
```

### Step 6: Assign bones = fsl.TractSkeleton(...)

```python
bones = fsl.TractSkeleton(in_file='a.nii', project_data=True)
```

### Step 7: Assign bones.inputs.threshold = 0.2

```python
bones.inputs.threshold = 0.2
```

### Step 8: Assign bones.inputs.distance_map = 'b.nii'

```python
bones.inputs.distance_map = 'b.nii'
```

### Step 9: Assign bones.inputs.data_file = 'b.nii'

```python
bones.inputs.data_file = 'b.nii'
```

**Verification:**
```python
assert bones.cmdline == 'tbss_skeleton -i a.nii -p 0.200 b.nii {} b.nii {}'.format(Info.standard_image('LowerCingulum_1mm.nii.gz'), os.path.join(newdir, 'b_skeletonised.nii'))
```

### Step 10: Assign bones.inputs.use_cingulum_mask = Undefined

```python
bones.inputs.use_cingulum_mask = Undefined
```

### Step 11: Assign bones.inputs.search_mask_file = 'a.nii'

```python
bones.inputs.search_mask_file = 'a.nii'
```

**Verification:**
```python
assert bones.cmdline == 'tbss_skeleton -i a.nii -p 0.200 b.nii a.nii b.nii %s' % os.path.join(newdir, 'b_skeletonised.nii')
```

### Step 12: Call skeletor.run()

```python
skeletor.run()
```

### Step 13: Call bones.run()

```python
bones.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
skeletor = fsl.TractSkeleton()
files, newdir = create_files_in_directory
assert skeletor.cmd == 'tbss_skeleton'
with pytest.raises(ValueError):
    skeletor.run()
skeletor.inputs.in_file = files[0]
skeletor.inputs.skeleton_file = True
assert skeletor.cmdline == 'tbss_skeleton -i a.nii -o %s' % os.path.join(newdir, 'a_skeleton.nii')
skeletor.inputs.skeleton_file = 'old_boney.nii'
assert skeletor.cmdline == 'tbss_skeleton -i a.nii -o old_boney.nii'
bones = fsl.TractSkeleton(in_file='a.nii', project_data=True)
with pytest.raises(ValueError):
    bones.run()
bones.inputs.threshold = 0.2
bones.inputs.distance_map = 'b.nii'
bones.inputs.data_file = 'b.nii'
assert bones.cmdline == 'tbss_skeleton -i a.nii -p 0.200 b.nii {} b.nii {}'.format(Info.standard_image('LowerCingulum_1mm.nii.gz'), os.path.join(newdir, 'b_skeletonised.nii'))
bones.inputs.use_cingulum_mask = Undefined
bones.inputs.search_mask_file = 'a.nii'
assert bones.cmdline == 'tbss_skeleton -i a.nii -p 0.200 b.nii a.nii b.nii %s' % os.path.join(newdir, 'b_skeletonised.nii')
```

## Next Steps


---

*Source: test_dti.py:335 | Complexity: Advanced | Last updated: 2026-05-18*