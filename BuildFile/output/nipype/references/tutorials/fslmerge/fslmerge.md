# How To: Fslmerge

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fslmerge

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `nipype.interfaces.fsl.utils`
- `nipype.interfaces.fsl`
- `nipype.testing.fixtures`

**Setup Required:**
```python
# Fixtures: create_files_in_directory_plus_output_type
```

## Step-by-Step Guide

### Step 1: Assign unknown = create_files_in_directory_plus_output_type

```python
filelist, outdir, _ = create_files_in_directory_plus_output_type
```

**Verification:**
```python
assert merger.cmd == 'fslmerge'
```

### Step 2: Assign merger = fsl.Merge(...)

```python
merger = fsl.Merge()
```

**Verification:**
```python
assert merger.cmdline == 'fslmerge -t foo_merged.nii %s' % ' '.join(filelist)
```

### Step 3: Assign merger.inputs.in_files = filelist

```python
merger.inputs.in_files = filelist
```

**Verification:**
```python
assert merger.cmdline == 'fslmerge -tr foo_merged.nii {} {:.2f}'.format(' '.join(filelist), 2.25)
```

### Step 4: Assign merger.inputs.merged_file = 'foo_merged.nii'

```python
merger.inputs.merged_file = 'foo_merged.nii'
```

**Verification:**
```python
assert merger2.cmdline == 'fslmerge -tr foo_merged.nii {} {:.2f}'.format(' '.join(filelist), 2.25)
```

### Step 5: Assign merger.inputs.dimension = 't'

```python
merger.inputs.dimension = 't'
```

### Step 6: Assign merger.inputs.output_type = 'NIFTI'

```python
merger.inputs.output_type = 'NIFTI'
```

**Verification:**
```python
assert merger.cmdline == 'fslmerge -t foo_merged.nii %s' % ' '.join(filelist)
```

### Step 7: Assign merger.inputs.tr = 2.25

```python
merger.inputs.tr = 2.25
```

**Verification:**
```python
assert merger.cmdline == 'fslmerge -tr foo_merged.nii {} {:.2f}'.format(' '.join(filelist), 2.25)
```

### Step 8: Assign merger2 = fsl.Merge(...)

```python
merger2 = fsl.Merge(in_files=filelist, merged_file='foo_merged.nii', dimension='t', output_type='NIFTI', tr=2.25)
```

**Verification:**
```python
assert merger2.cmdline == 'fslmerge -tr foo_merged.nii {} {:.2f}'.format(' '.join(filelist), 2.25)
```

### Step 9: Call merger.run()

```python
merger.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
filelist, outdir, _ = create_files_in_directory_plus_output_type
merger = fsl.Merge()
assert merger.cmd == 'fslmerge'
with pytest.raises(ValueError):
    merger.run()
merger.inputs.in_files = filelist
merger.inputs.merged_file = 'foo_merged.nii'
merger.inputs.dimension = 't'
merger.inputs.output_type = 'NIFTI'
assert merger.cmdline == 'fslmerge -t foo_merged.nii %s' % ' '.join(filelist)
merger.inputs.tr = 2.25
assert merger.cmdline == 'fslmerge -tr foo_merged.nii {} {:.2f}'.format(' '.join(filelist), 2.25)
merger2 = fsl.Merge(in_files=filelist, merged_file='foo_merged.nii', dimension='t', output_type='NIFTI', tr=2.25)
assert merger2.cmdline == 'fslmerge -tr foo_merged.nii {} {:.2f}'.format(' '.join(filelist), 2.25)
```

## Next Steps


---

*Source: test_utils.py:55 | Complexity: Advanced | Last updated: 2026-05-18*