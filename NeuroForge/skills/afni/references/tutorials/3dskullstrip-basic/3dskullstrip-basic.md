# How To: 3Dskullstrip Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dSkullStrip basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data, dset_name
```

## Step-by-Step Guide

### Step 1: Assign ifile = getattr(...)

```python
ifile = getattr(data, dset_name)
```

### Step 2: Assign ofile = value

```python
ofile = data.outdir / 'out_ss.nii.gz'
```

### Step 3: Assign cmd = '3dSkullStrip -prefix {ofile} -input {ifile}'

```python
cmd = '3dSkullStrip -prefix {ofile} -input {ifile}'
```

### Step 4: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 5: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd)
```

### Step 6: Call differ.run()

```python
differ.run()
```


## Complete Example

```python
# Setup
# Fixtures: data, dset_name

# Workflow
ifile = getattr(data, dset_name)
ofile = data.outdir / 'out_ss.nii.gz'
cmd = '3dSkullStrip -prefix {ofile} -input {ifile}'
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_3dSkullStrip.py:16 | Complexity: Intermediate | Last updated: 2026-05-18*