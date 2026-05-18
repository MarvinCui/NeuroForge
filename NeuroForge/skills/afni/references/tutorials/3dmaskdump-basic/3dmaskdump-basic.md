# How To: 3Dmaskdump Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dmaskdump basic

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

### Step 1: Assign outfile_path = value

```python
outfile_path = data.outdir / 'Vrel_tstats.txt'
```

### Step 2: Assign cmd = '\n    3dmaskdump\n        -noijk\n        -mask {data.mask} {data.epi}\n        > {outfile_path}\n    '

```python
cmd = '\n    3dmaskdump\n        -noijk\n        -mask {data.mask} {data.epi}\n        > {outfile_path}\n    '
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
outfile_path = data.outdir / 'Vrel_tstats.txt'
cmd = '\n    3dmaskdump\n        -noijk\n        -mask {data.mask} {data.epi}\n        > {outfile_path}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_3dmaskdump.py:13 | Complexity: Intermediate | Last updated: 2026-05-18*