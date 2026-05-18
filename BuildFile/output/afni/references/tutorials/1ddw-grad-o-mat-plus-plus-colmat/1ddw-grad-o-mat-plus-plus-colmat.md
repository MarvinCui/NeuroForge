# How To: 1Ddw Grad O Mat Plus Plus Colmat

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 1dDW Grad o Mat plus plus colmat

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

### Step 1: Assign outfile = value

```python
outfile = data.outdir / 'o.1dDW_Grad_o_Mat++_BMAT.txt'
```

### Step 2: Assign cmd = value

```python
cmd = f"\n    1dDW_Grad_o_Mat++\n        -echo_edu\n        -in_row_vec {data.bvec}'[2..32]'\n        -in_bvals {data.bval}'[2..32]'\n        -flip_y\n        -out_col_matA {outfile}\n    "
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
outfile = data.outdir / 'o.1dDW_Grad_o_Mat++_BMAT.txt'
cmd = f"\n    1dDW_Grad_o_Mat++\n        -echo_edu\n        -in_row_vec {data.bvec}'[2..32]'\n        -in_bvals {data.bval}'[2..32]'\n        -flip_y\n        -out_col_matA {outfile}\n    "
cmd = ' '.join(cmd.split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_ptaylor.py:55 | Complexity: Intermediate | Last updated: 2026-05-18*