# How To: Createnifti

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test CreateNifti

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `os`
- `nibabel`
- `nipype.algorithms`
- `nipype.utils.filemanip`
- `nipype.testing.fixtures`
- `nipype.testing`

**Setup Required:**
```python
# Fixtures: create_analyze_pair_file_in_directory
```

## Step-by-Step Guide

### Step 1: Assign unknown = create_analyze_pair_file_in_directory

```python
filelist, outdir = create_analyze_pair_file_in_directory
```

**Verification:**
```python
assert os.path.exists(result.outputs.nifti_file)
```

### Step 2: Assign create_nifti = misc.CreateNifti(...)

```python
create_nifti = misc.CreateNifti()
```

**Verification:**
```python
assert nb.load(result.outputs.nifti_file)
```

### Step 3: Assign create_nifti.inputs.header_file = value

```python
create_nifti.inputs.header_file = filelist[0]
```

### Step 4: Assign create_nifti.inputs.data_file = fname_presuffix(...)

```python
create_nifti.inputs.data_file = fname_presuffix(filelist[0], '', '.img', use_ext=False)
```

### Step 5: Assign result = create_nifti.run(...)

```python
result = create_nifti.run()
```

**Verification:**
```python
assert os.path.exists(result.outputs.nifti_file)
```

### Step 6: Call create_nifti.run()

```python
create_nifti.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_analyze_pair_file_in_directory

# Workflow
filelist, outdir = create_analyze_pair_file_in_directory
create_nifti = misc.CreateNifti()
with pytest.raises(ValueError):
    create_nifti.run()
create_nifti.inputs.header_file = filelist[0]
create_nifti.inputs.data_file = fname_presuffix(filelist[0], '', '.img', use_ext=False)
result = create_nifti.run()
assert os.path.exists(result.outputs.nifti_file)
assert nb.load(result.outputs.nifti_file)
```

## Next Steps


---

*Source: test_misc.py:15 | Complexity: Intermediate | Last updated: 2026-05-18*