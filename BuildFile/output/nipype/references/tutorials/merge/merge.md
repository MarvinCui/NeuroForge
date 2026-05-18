# How To: Merge

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test merge

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign merge = Merge(...)

```python
merge = Merge()
```

**Verification:**
```python
assert merge.cmd == cmd
```

### Step 2: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert merge.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 4: Assign file1 = example_data(...)

```python
file1 = example_data('im2.nii')
```

### Step 5: Assign file2 = example_data(...)

```python
file2 = example_data('im3.nii')
```

### Step 6: Assign merge.inputs.in_file = in_file

```python
merge.inputs.in_file = in_file
```

### Step 7: Assign merge.inputs.merge_files = value

```python
merge.inputs.merge_files = [file1, file2]
```

### Step 8: Assign merge.inputs.dimension = 2

```python
merge.inputs.dimension = 2
```

### Step 9: Assign merge.inputs.output_datatype = 'float'

```python
merge.inputs.output_datatype = 'float'
```

### Step 10: Assign cmd_tmp = '{cmd} {in_file} -merge 2 2 {f1} {f2} -odt float {out_file}'

```python
cmd_tmp = '{cmd} {in_file} -merge 2 2 {f1} {f2} -odt float {out_file}'
```

### Step 11: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, f1=file1, f2=file2, out_file='im1_merged.nii')
```

**Verification:**
```python
assert merge.cmdline == expected_cmd
```

### Step 12: Call merge.run()

```python
merge.run()
```


## Complete Example

```python
# Workflow
merge = Merge()
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
assert merge.cmd == cmd
with pytest.raises(ValueError):
    merge.run()
in_file = example_data('im1.nii')
file1 = example_data('im2.nii')
file2 = example_data('im3.nii')
merge.inputs.in_file = in_file
merge.inputs.merge_files = [file1, file2]
merge.inputs.dimension = 2
merge.inputs.output_datatype = 'float'
cmd_tmp = '{cmd} {in_file} -merge 2 2 {f1} {f2} -odt float {out_file}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, f1=file1, f2=file2, out_file='im1_merged.nii')
assert merge.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_maths.py:122 | Complexity: Advanced | Last updated: 2026-05-18*