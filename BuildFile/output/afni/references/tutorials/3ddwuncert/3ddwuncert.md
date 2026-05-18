# How To: 3Ddwuncert

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dDWUncert

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
opref = data.outdir / 'o.3dDWUncert'
```

### Step 2: Assign cmd = value

```python
cmd = f'\n    3dDWUncert\n        -echo_edu\n        -inset {data.AVEB0_DWI}\n        -mask {data.mask_DWI}\n        -pt_choose_seed 5\n        -prefix {opref}\n        -input {data.tests_data_dir / fatdir2}/DT\n        -bmatrix_FULL {data.grad_BMAT}\n        -iters 10\n\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.split())
```

### Step 4: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, kwargs_log={'append_to_ignored': [' min', 'Nvox progress proxy count']})
```

### Step 5: Call differ.run()

```python
differ.run(timeout=60)
```


## Complete Example

```python
# Setup
# Fixtures: data, ptaylor_env

# Workflow
opref = data.outdir / 'o.3dDWUncert'
cmd = f'\n    3dDWUncert\n        -echo_edu\n        -inset {data.AVEB0_DWI}\n        -mask {data.mask_DWI}\n        -pt_choose_seed 5\n        -prefix {opref}\n        -input {data.tests_data_dir / fatdir2}/DT\n        -bmatrix_FULL {data.grad_BMAT}\n        -iters 10\n\n    '
cmd = ' '.join(cmd.split())
differ = tools.OutputDiffer(data, cmd, kwargs_log={'append_to_ignored': [' min', 'Nvox progress proxy count']})
differ.run(timeout=60)
```

## Next Steps


---

*Source: test_ptaylor.py:217 | Complexity: Intermediate | Last updated: 2026-05-18*