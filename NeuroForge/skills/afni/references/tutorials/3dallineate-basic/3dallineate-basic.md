# How To: 3Dallineate Basic

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dAllineate basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `afni_test_utils.misc`
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data, python_interpreter
```

## Step-by-Step Guide

### Step 1: Assign outname = 'aligned'

```python
outname = 'aligned'
```

### Step 2: Assign outfile = value

```python
outfile = data.outdir / (outname + '.nii.gz')
```

### Step 3: Assign out_1d = value

```python
out_1d = outfile.parent / (outfile.stem.split('.')[0] + '.1D')
```

### Step 4: Assign cmd = "\n    3dAllineate\n        -base {data.anat1}\n        -source {data.epi}'[0]'\n        -prefix {outfile}\n        -1Dparam_save {out_1d}\n        -maxrot 2\n        -maxshf 1\n        -nmatch 20\n        -conv 2\n        -cost lpc\n    "

```python
cmd = "\n    3dAllineate\n        -base {data.anat1}\n        -source {data.epi}'[0]'\n        -prefix {outfile}\n        -1Dparam_save {out_1d}\n        -maxrot 2\n        -maxshf 1\n        -nmatch 20\n        -conv 2\n        -cost lpc\n    "
```

### Step 5: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 6: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, python_interpreter=python_interpreter, kwargs_log={'append_to_ignored': ['Output dataset', '++ Wrote -1Dparam_save', 'total CPU time']})
```

### Step 7: Call differ.run()

```python
differ.run()
```


## Complete Example

```python
# Setup
# Fixtures: data, python_interpreter

# Workflow
outname = 'aligned'
if OMP:
    outname += '_with_omp'
outfile = data.outdir / (outname + '.nii.gz')
out_1d = outfile.parent / (outfile.stem.split('.')[0] + '.1D')
cmd = "\n    3dAllineate\n        -base {data.anat1}\n        -source {data.epi}'[0]'\n        -prefix {outfile}\n        -1Dparam_save {out_1d}\n        -maxrot 2\n        -maxshf 1\n        -nmatch 20\n        -conv 2\n        -cost lpc\n    "
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd, python_interpreter=python_interpreter, kwargs_log={'append_to_ignored': ['Output dataset', '++ Wrote -1Dparam_save', 'total CPU time']})
differ.run()
```

## Next Steps


---

*Source: test_3dAllineate.py:22 | Complexity: Intermediate | Last updated: 2026-05-18*