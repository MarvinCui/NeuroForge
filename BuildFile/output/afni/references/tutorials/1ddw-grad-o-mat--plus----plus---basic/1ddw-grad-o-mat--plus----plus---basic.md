# How To: 1Ddw Grad O Mat  Plus    Plus   Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 1dDW Grad o Mat  plus    plus   basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data
```

## Step-by-Step Guide

### Step 1: Assign outfile = value

```python
outfile = data.outdir / 'GRADS_30.dat'
```

### Step 2: Assign cmd = "\n    1dDW_Grad_o_Mat++ \n    -in_row_vec {data.bvec}'[2..32]' \n    -flip_y  \n    -out_col_vec {outfile}\n    "

```python
cmd = "\n    1dDW_Grad_o_Mat++ \n    -in_row_vec {data.bvec}'[2..32]' \n    -flip_y  \n    -out_col_vec {outfile}\n    "
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
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
# Fixtures: data

# Workflow
outfile = data.outdir / 'GRADS_30.dat'
cmd = "\n    1dDW_Grad_o_Mat++ \n    -in_row_vec {data.bvec}'[2..32]' \n    -flip_y  \n    -out_col_vec {outfile}\n    "
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_1dDW_Grad_o_Mat++.py:7 | Complexity: Intermediate | Last updated: 2026-05-18*