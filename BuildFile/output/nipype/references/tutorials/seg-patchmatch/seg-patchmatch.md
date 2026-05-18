# How To: Seg Patchmatch

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test seg patchmatch

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign seg_patchmatch = PatchMatch(...)

```python
seg_patchmatch = PatchMatch()
```

**Verification:**
```python
assert seg_patchmatch.cmd == cmd
```

### Step 2: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_PatchMatch', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert seg_patchmatch.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 4: Assign mask_file = example_data(...)

```python
mask_file = example_data('im2.nii')
```

### Step 5: Assign db_file = example_data(...)

```python
db_file = example_data('db.xml')
```

### Step 6: Assign seg_patchmatch.inputs.in_file = in_file

```python
seg_patchmatch.inputs.in_file = in_file
```

### Step 7: Assign seg_patchmatch.inputs.mask_file = mask_file

```python
seg_patchmatch.inputs.mask_file = mask_file
```

### Step 8: Assign seg_patchmatch.inputs.database_file = db_file

```python
seg_patchmatch.inputs.database_file = db_file
```

### Step 9: Assign cmd_tmp = '{cmd} -i {in_file} -m {mask_file} -db {db} -o {out_file}'

```python
cmd_tmp = '{cmd} -i {in_file} -m {mask_file} -db {db} -o {out_file}'
```

### Step 10: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, mask_file=mask_file, db=db_file, out_file='im1_pm.nii.gz')
```

**Verification:**
```python
assert seg_patchmatch.cmdline == expected_cmd
```

### Step 11: Call seg_patchmatch.run()

```python
seg_patchmatch.run()
```


## Complete Example

```python
# Workflow
seg_patchmatch = PatchMatch()
cmd = get_custom_path('seg_PatchMatch', env_dir='NIFTYSEGDIR')
assert seg_patchmatch.cmd == cmd
with pytest.raises(ValueError):
    seg_patchmatch.run()
in_file = example_data('im1.nii')
mask_file = example_data('im2.nii')
db_file = example_data('db.xml')
seg_patchmatch.inputs.in_file = in_file
seg_patchmatch.inputs.mask_file = mask_file
seg_patchmatch.inputs.database_file = db_file
cmd_tmp = '{cmd} -i {in_file} -m {mask_file} -db {db} -o {out_file}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, mask_file=mask_file, db=db_file, out_file='im1_pm.nii.gz')
assert seg_patchmatch.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_extra_PatchMatch.py:15 | Complexity: Advanced | Last updated: 2026-05-18*