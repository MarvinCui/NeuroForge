# How To: 3Dmaskave Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dmaskave basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `sys`
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data
```

## Step-by-Step Guide

### Step 1: Assign outfile_prefix = value

```python
outfile_prefix = data.outdir / 'anat_roi_resam.nii.gz'
```

### Step 2: Assign out_1d = value

```python
out_1d = data.outdir / 'epi_avg.1D'
```

### Step 3: Assign cmd = '\n    3dmaskave\n        -mask {data.mask}\n        -quiet {data.epi}\n        > {out_1d}\n    '

```python
cmd = '\n    3dmaskave\n        -mask {data.mask}\n        -quiet {data.epi}\n        > {out_1d}\n    '
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
# Fixtures: data

# Workflow
outfile_prefix = data.outdir / 'anat_roi_resam.nii.gz'
out_1d = data.outdir / 'epi_avg.1D'
cmd = '\n    3dmaskave\n        -mask {data.mask}\n        -quiet {data.epi}\n        > {out_1d}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_3dmaskave.py:13 | Complexity: Intermediate | Last updated: 2026-05-18*