# How To: Regaverage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RegAverage inputs

## Prerequisites

**Required Modules:**
- `regutils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), avg_files=dict(argstr='-avg %s', position=1, sep=' ', xor=['avg_lts_files', 'avg_ref_file', 'demean1_ref_file', 'demean2_ref_file', 'demean3_ref_file', 'warp_files']), avg_lts_files=dict(argstr='-avg_lts %s', position=1, sep=' ', xor=['avg_files', 'avg_ref_file', 'demean1_ref_file', 'demean2_ref_file', 'demean3_ref_file', 'warp_files']), avg_ref_file=dict(argstr='-avg_tran %s', extensions=None, position=1, requires=['warp_files'], xor=['avg_files', 'avg_lts_files', 'demean1_ref_file', 'demean2_ref_file', 'demean3_ref_file']), demean1_ref_file=dict(argstr='-demean1 %s', extensions=None, position=1, requires=['warp_files'], xor=['avg_files', 'avg_lts_files', 'avg_ref_file', 'demean2_ref_file', 'demean3_ref_file']), demean2_ref_file=dict(argstr='-demean2 %s', extensions=None, position=1, requires=['warp_files'], xor=['avg_files', 'avg_lts_files', 'avg_ref_file', 'demean1_ref_file', 'demean3_ref_file']), demean3_ref_file=dict(argstr='-demean3 %s', extensions=None, position=1, requires=['warp_files'], xor=['avg_files', 'avg_lts_files', 'avg_ref_file', 'demean1_ref_file', 'demean2_ref_file']), environ=dict(nohash=True, usedefault=True), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='%s', extensions=None, genfile=True, position=0), warp_files=dict(argstr='%s', position=-1, sep=' ', xor=['avg_files', 'avg_lts_files']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), avg_files=dict(argstr='-avg %s', position=1, sep=' ', xor=['avg_lts_files', 'avg_ref_file', 'demean1_ref_file', 'demean2_ref_file', 'demean3_ref_file', 'warp_files']), avg_lts_files=dict(argstr='-avg_lts %s', position=1, sep=' ', xor=['avg_files', 'avg_ref_file', 'demean1_ref_file', 'demean2_ref_file', 'demean3_ref_file', 'warp_files']), avg_ref_file=dict(argstr='-avg_tran %s', extensions=None, position=1, requires=['warp_files'], xor=['avg_files', 'avg_lts_files', 'demean1_ref_file', 'demean2_ref_file', 'demean3_ref_file']), demean1_ref_file=dict(argstr='-demean1 %s', extensions=None, position=1, requires=['warp_files'], xor=['avg_files', 'avg_lts_files', 'avg_ref_file', 'demean2_ref_file', 'demean3_ref_file']), demean2_ref_file=dict(argstr='-demean2 %s', extensions=None, position=1, requires=['warp_files'], xor=['avg_files', 'avg_lts_files', 'avg_ref_file', 'demean1_ref_file', 'demean3_ref_file']), demean3_ref_file=dict(argstr='-demean3 %s', extensions=None, position=1, requires=['warp_files'], xor=['avg_files', 'avg_lts_files', 'avg_ref_file', 'demean1_ref_file', 'demean2_ref_file']), environ=dict(nohash=True, usedefault=True), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='%s', extensions=None, genfile=True, position=0), warp_files=dict(argstr='%s', position=-1, sep=' ', xor=['avg_files', 'avg_lts_files']))
```

## Next Steps


---

*Source: test_auto_RegAverage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*