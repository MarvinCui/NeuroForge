# How To: 3Ddwitodt

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dDWItoDT

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `afni_test_utils`
- `pathlib`
- `pytest`
- `sys`

**Setup Required:**
```python
# Fixtures: data, ptaylor_env
```

## Step-by-Step Guide

### Step 1: Assign opref = value

```python
opref = data.outdir / '3dDWItoDT'
```

### Step 2: Assign cmd = value

```python
cmd = f'\n    3dDWItoDT\n        -echo_edu\n        -prefix {opref}\n        -mask {data.mask_DWI}\n        -eigs\n        -scale_out_1000\n        -sep_dsets\n        -linear\n        -bmatrix_FULL {data.grad_BMAT}\n        {data.AVEB0_DWI}\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.split())
```

### Step 4: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, kwargs_scans={'data_kwargs': {'rtol': 0.01}})
```

### Step 5: Call differ.run()

```python
differ.run(timeout=90)
```


## Complete Example

```python
# Setup
# Fixtures: data, ptaylor_env

# Workflow
opref = data.outdir / '3dDWItoDT'
cmd = f'\n    3dDWItoDT\n        -echo_edu\n        -prefix {opref}\n        -mask {data.mask_DWI}\n        -eigs\n        -scale_out_1000\n        -sep_dsets\n        -linear\n        -bmatrix_FULL {data.grad_BMAT}\n        {data.AVEB0_DWI}\n    '
cmd = ' '.join(cmd.split())
differ = tools.OutputDiffer(data, cmd, kwargs_scans={'data_kwargs': {'rtol': 0.01}})
differ.run(timeout=90)
```

## Next Steps


---

*Source: test_ptaylor.py:88 | Complexity: Intermediate | Last updated: 2026-05-18*