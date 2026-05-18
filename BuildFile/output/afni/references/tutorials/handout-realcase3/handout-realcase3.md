# How To: Handout Realcase3

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test handout realcase3

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `afni_test_utils`
- `pytest`

**Setup Required:**
```python
# Fixtures: data, python_interpreter
```

## Step-by-Step Guide

### Step 1: Assign subj = 'FT'

```python
subj = 'FT'
```

### Step 2: Assign cmd = '\n    afni_proc.py\n        -subj_id {subj}\n        -script proc.{subj}\n        -scr_overwrite\n        -blocks tshift align tlrc volreg blur mask scale regress\n        -copy_anat {data.anat}\n        -dsets {data.epi_1} {data.epi_2} {data.epi_3}\n        -volreg_align_to MIN_OUTLIER\n        -volreg_align_e2a\n        -volreg_tlrc_warp\n        -blur_size 4.0\n    '

```python
cmd = '\n    afni_proc.py\n        -subj_id {subj}\n        -script proc.{subj}\n        -scr_overwrite\n        -blocks tshift align tlrc volreg blur mask scale regress\n        -copy_anat {data.anat}\n        -dsets {data.epi_1} {data.epi_2} {data.epi_3}\n        -volreg_align_to MIN_OUTLIER\n        -volreg_align_e2a\n        -volreg_tlrc_warp\n        -blur_size 4.0\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 4: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, workdir=data.outdir, python_interpreter=python_interpreter, text_file_patterns=['.FT'], kwargs_text_files={'ignore_patterns': ['auto-gener']})
```

### Step 5: Call differ.run()

```python
differ.run()
```


## Complete Example

```python
# Setup
# Fixtures: data, python_interpreter

# Workflow
subj = 'FT'
cmd = '\n    afni_proc.py\n        -subj_id {subj}\n        -script proc.{subj}\n        -scr_overwrite\n        -blocks tshift align tlrc volreg blur mask scale regress\n        -copy_anat {data.anat}\n        -dsets {data.epi_1} {data.epi_2} {data.epi_3}\n        -volreg_align_to MIN_OUTLIER\n        -volreg_align_e2a\n        -volreg_tlrc_warp\n        -blur_size 4.0\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd, workdir=data.outdir, python_interpreter=python_interpreter, text_file_patterns=['.FT'], kwargs_text_files={'ignore_patterns': ['auto-gener']})
differ.run()
```

## Next Steps


---

*Source: test_afni_proc.py:68 | Complexity: Intermediate | Last updated: 2026-05-18*