# How To: Ms Lda Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MS LDA inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), conform=dict(argstr='-conform'), environ=dict(nohash=True, usedefault=True), images=dict(argstr='%s', copyfile=False, mandatory=True, position=-1), label_file=dict(argstr='-label %s', extensions=None), lda_labels=dict(argstr='-lda %s', mandatory=True, sep=' '), mask_file=dict(argstr='-mask %s', extensions=None), shift=dict(argstr='-shift %d'), subjects_dir=dict(), use_weights=dict(argstr='-W'), vol_synth_file=dict(argstr='-synth %s', extensions=None, mandatory=True), weight_file=dict(argstr='-weight %s', extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), conform=dict(argstr='-conform'), environ=dict(nohash=True, usedefault=True), images=dict(argstr='%s', copyfile=False, mandatory=True, position=-1), label_file=dict(argstr='-label %s', extensions=None), lda_labels=dict(argstr='-lda %s', mandatory=True, sep=' '), mask_file=dict(argstr='-mask %s', extensions=None), shift=dict(argstr='-shift %d'), subjects_dir=dict(), use_weights=dict(argstr='-W'), vol_synth_file=dict(argstr='-synth %s', extensions=None, mandatory=True), weight_file=dict(argstr='-weight %s', extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_MS_LDA.py:6 | Complexity: Beginner | Last updated: 2026-05-18*