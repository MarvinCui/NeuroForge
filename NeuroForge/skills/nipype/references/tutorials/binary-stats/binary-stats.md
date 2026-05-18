# How To: Binary Stats

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test for the seg_stats interfaces

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: 'Test for the seg_stats interfaces'

```python
'Test for the seg_stats interfaces'
```

**Verification:**
```python
assert binarys.cmd == cmd
```

### Step 2: Assign binarys = BinaryStats(...)

```python
binarys = BinaryStats()
```

**Verification:**
```python
assert binarys.cmdline == expected_cmd
```

### Step 3: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_stats', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert binarys.cmd == cmd
```

### Step 4: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 5: Assign binarys.inputs.in_file = in_file

```python
binarys.inputs.in_file = in_file
```

### Step 6: Assign binarys.inputs.operand_value = 2

```python
binarys.inputs.operand_value = 2
```

### Step 7: Assign binarys.inputs.operation = 'sa'

```python
binarys.inputs.operation = 'sa'
```

### Step 8: Assign expected_cmd = value

```python
expected_cmd = f'{cmd} {in_file} -sa 2.00000000'
```

**Verification:**
```python
assert binarys.cmdline == expected_cmd
```

### Step 9: Call binarys.run()

```python
binarys.run()
```


## Complete Example

```python
# Workflow
'Test for the seg_stats interfaces'
binarys = BinaryStats()
cmd = get_custom_path('seg_stats', env_dir='NIFTYSEGDIR')
assert binarys.cmd == cmd
with pytest.raises(ValueError):
    binarys.run()
in_file = example_data('im1.nii')
binarys.inputs.in_file = in_file
binarys.inputs.operand_value = 2
binarys.inputs.operation = 'sa'
expected_cmd = f'{cmd} {in_file} -sa 2.00000000'
assert binarys.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_stats.py:37 | Complexity: Advanced | Last updated: 2026-05-18*