# How To: Handout Realcase2

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the command in the afni_proc.py handout (real case 2).

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

### Step 1: 'Test the command in the afni_proc.py handout (real case 2).'

```python
'Test the command in the afni_proc.py handout (real case 2).'
```

### Step 2: Assign subj = 'FT'

```python
subj = 'FT'
```

### Step 3: Assign cmd = "\n    afni_proc.py\n        -subj_id {subj}\n        -script proc.{subj}\n        -scr_overwrite\n        -blocks tshift align tlrc volreg blur mask scale regress\n        -copy_anat {data.anat}\n        -dsets {data.epi_1} {data.epi_2} {data.epi_3}\n        -volreg_align_to MIN_OUTLIER\n        -volreg_align_e2a\n        -volreg_tlrc_warp\n        -blur_size 4.0\n        -tcat_remove_first_trs 2\n        -regress_stim_times {data.av1_vis} {data.av2_aud}\n        -regress_stim_labels vis aud\n        -regress_basis 'BLOCK(20,1)'\n        -regress_censor_motion 0.3\n        -regress_opts_3dD\n        -jobs 2\n        -gltsym 'SYM: vis\n        -aud'\n        -glt_label 1 V\n        -A\n        -gltsym 'SYM: 0.5*vis +0.5*aud'\n        -glt_label 2 mean.VA\n        -regress_compute_fitts\n        -regress_make_ideal_sum sum_ideal.1D\n        -regress_est_blur_epits\n        -regress_est_blur_errts\n        -regress_run_clustsim yes\n    "

```python
cmd = "\n    afni_proc.py\n        -subj_id {subj}\n        -script proc.{subj}\n        -scr_overwrite\n        -blocks tshift align tlrc volreg blur mask scale regress\n        -copy_anat {data.anat}\n        -dsets {data.epi_1} {data.epi_2} {data.epi_3}\n        -volreg_align_to MIN_OUTLIER\n        -volreg_align_e2a\n        -volreg_tlrc_warp\n        -blur_size 4.0\n        -tcat_remove_first_trs 2\n        -regress_stim_times {data.av1_vis} {data.av2_aud}\n        -regress_stim_labels vis aud\n        -regress_basis 'BLOCK(20,1)'\n        -regress_censor_motion 0.3\n        -regress_opts_3dD\n        -jobs 2\n        -gltsym 'SYM: vis\n        -aud'\n        -glt_label 1 V\n        -A\n        -gltsym 'SYM: 0.5*vis +0.5*aud'\n        -glt_label 2 mean.VA\n        -regress_compute_fitts\n        -regress_make_ideal_sum sum_ideal.1D\n        -regress_est_blur_epits\n        -regress_est_blur_errts\n        -regress_run_clustsim yes\n    "
```

### Step 4: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 5: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, workdir=data.outdir, python_interpreter=python_interpreter, text_file_patterns=['.FT'], kwargs_text_files={'ignore_patterns': ['auto-gener']}, kwargs_log={'append_to_ignored': ['-']})
```

### Step 6: Call differ.run()

```python
differ.run()
```


## Complete Example

```python
# Setup
# Fixtures: data, python_interpreter

# Workflow
'Test the command in the afni_proc.py handout (real case 2).'
subj = 'FT'
cmd = "\n    afni_proc.py\n        -subj_id {subj}\n        -script proc.{subj}\n        -scr_overwrite\n        -blocks tshift align tlrc volreg blur mask scale regress\n        -copy_anat {data.anat}\n        -dsets {data.epi_1} {data.epi_2} {data.epi_3}\n        -volreg_align_to MIN_OUTLIER\n        -volreg_align_e2a\n        -volreg_tlrc_warp\n        -blur_size 4.0\n        -tcat_remove_first_trs 2\n        -regress_stim_times {data.av1_vis} {data.av2_aud}\n        -regress_stim_labels vis aud\n        -regress_basis 'BLOCK(20,1)'\n        -regress_censor_motion 0.3\n        -regress_opts_3dD\n        -jobs 2\n        -gltsym 'SYM: vis\n        -aud'\n        -glt_label 1 V\n        -A\n        -gltsym 'SYM: 0.5*vis +0.5*aud'\n        -glt_label 2 mean.VA\n        -regress_compute_fitts\n        -regress_make_ideal_sum sum_ideal.1D\n        -regress_est_blur_epits\n        -regress_est_blur_errts\n        -regress_run_clustsim yes\n    "
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd, workdir=data.outdir, python_interpreter=python_interpreter, text_file_patterns=['.FT'], kwargs_text_files={'ignore_patterns': ['auto-gener']}, kwargs_log={'append_to_ignored': ['-']})
differ.run()
```

## Next Steps


---

*Source: test_afni_proc.py:17 | Complexity: Intermediate | Last updated: 2026-05-18*