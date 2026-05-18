# How To: Tcorr1D Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TCorr1D inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), ktaub=dict(argstr=' -ktaub', position=1, xor=['pearson', 'spearman', 'quadrant']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=True, name_source='xset', name_template='%s_correlation.nii.gz'), outputtype=dict(), pearson=dict(argstr=' -pearson', position=1, xor=['spearman', 'quadrant', 'ktaub']), quadrant=dict(argstr=' -quadrant', position=1, xor=['pearson', 'spearman', 'ktaub']), spearman=dict(argstr=' -spearman', position=1, xor=['pearson', 'quadrant', 'ktaub']), xset=dict(argstr=' %s', copyfile=False, extensions=None, mandatory=True, position=-2), y_1d=dict(argstr=' %s', extensions=None, mandatory=True, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), ktaub=dict(argstr=' -ktaub', position=1, xor=['pearson', 'spearman', 'quadrant']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=True, name_source='xset', name_template='%s_correlation.nii.gz'), outputtype=dict(), pearson=dict(argstr=' -pearson', position=1, xor=['spearman', 'quadrant', 'ktaub']), quadrant=dict(argstr=' -quadrant', position=1, xor=['pearson', 'spearman', 'ktaub']), spearman=dict(argstr=' -spearman', position=1, xor=['pearson', 'quadrant', 'ktaub']), xset=dict(argstr=' %s', copyfile=False, extensions=None, mandatory=True, position=-2), y_1d=dict(argstr=' %s', extensions=None, mandatory=True, position=-1))
```

## Next Steps


---

*Source: test_auto_TCorr1D.py:6 | Complexity: Beginner | Last updated: 2026-05-18*