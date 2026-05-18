# How To: Synthesizeflash Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SynthesizeFLASH inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixed_weighting=dict(argstr='-w', position=1), flip_angle=dict(argstr='%.2f', mandatory=True, position=3), out_file=dict(argstr='%s', extensions=None, genfile=True), pd_image=dict(argstr='%s', extensions=None, mandatory=True, position=6), subjects_dir=dict(), t1_image=dict(argstr='%s', extensions=None, mandatory=True, position=5), te=dict(argstr='%.3f', mandatory=True, position=4), tr=dict(argstr='%.2f', mandatory=True, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fixed_weighting=dict(argstr='-w', position=1), flip_angle=dict(argstr='%.2f', mandatory=True, position=3), out_file=dict(argstr='%s', extensions=None, genfile=True), pd_image=dict(argstr='%s', extensions=None, mandatory=True, position=6), subjects_dir=dict(), t1_image=dict(argstr='%s', extensions=None, mandatory=True, position=5), te=dict(argstr='%.3f', mandatory=True, position=4), tr=dict(argstr='%.2f', mandatory=True, position=2))
```

## Next Steps


---

*Source: test_auto_SynthesizeFLASH.py:6 | Complexity: Beginner | Last updated: 2026-05-18*