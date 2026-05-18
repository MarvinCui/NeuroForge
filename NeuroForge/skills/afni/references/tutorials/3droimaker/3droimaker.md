# How To: 3Droimaker

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3dROIMaker

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
opref = data.outdir / 'o.3dROIMaker'
```

### Step 2: Assign cmd = value

```python
cmd = f'\n    3dROIMaker\n        -echo_edu\n        -nifti\n        -inset {data.SOME_ICA_NETS_in_DWI}\n        -thresh 3.0\n        -volthr 130\n        -inflate 2\n        -wm_skel {data.DT_FA}\n        -skel_thr 0.2\n        -skel_stop\n        -mask {data.mask_DWI}\n        -prefix {opref}\n        -overwrite\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.split())
```

### Step 4: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd)
```

### Step 5: Call differ.run()

```python
differ.run()
```


## Complete Example

```python
# Setup
# Fixtures: data, ptaylor_env

# Workflow
opref = data.outdir / 'o.3dROIMaker'
cmd = f'\n    3dROIMaker\n        -echo_edu\n        -nifti\n        -inset {data.SOME_ICA_NETS_in_DWI}\n        -thresh 3.0\n        -volthr 130\n        -inflate 2\n        -wm_skel {data.DT_FA}\n        -skel_thr 0.2\n        -skel_stop\n        -mask {data.mask_DWI}\n        -prefix {opref}\n        -overwrite\n    '
cmd = ' '.join(cmd.split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_ptaylor.py:112 | Complexity: Intermediate | Last updated: 2026-05-18*