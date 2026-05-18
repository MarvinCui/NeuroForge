# How To: Unary Stats

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
assert unarys.cmd == cmd
```

### Step 2: Assign unarys = UnaryStats(...)

```python
unarys = UnaryStats()
```

**Verification:**
```python
assert unarys.cmdline == expected_cmd
```

### Step 3: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_stats', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert unarys.cmd == cmd
```

### Step 4: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 5: Assign unarys.inputs.in_file = in_file

```python
unarys.inputs.in_file = in_file
```

### Step 6: Assign unarys.inputs.operation = 'a'

```python
unarys.inputs.operation = 'a'
```

### Step 7: Assign expected_cmd = value

```python
expected_cmd = f'{cmd} {in_file} -a'
```

**Verification:**
```python
assert unarys.cmdline == expected_cmd
```

### Step 8: Call unarys.run()

```python
unarys.run()
```


## Complete Example

```python
# Workflow
'Test for the seg_stats interfaces'
unarys = UnaryStats()
cmd = get_custom_path('seg_stats', env_dir='NIFTYSEGDIR')
assert unarys.cmd == cmd
with pytest.raises(ValueError):
    unarys.run()
in_file = example_data('im1.nii')
unarys.inputs.in_file = in_file
unarys.inputs.operation = 'a'
expected_cmd = f'{cmd} {in_file} -a'
assert unarys.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_stats.py:13 | Complexity: Advanced | Last updated: 2026-05-18*