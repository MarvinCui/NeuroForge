# How To: Automask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Automask inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), brain_file=dict(argstr='-apply_prefix %s', extensions=None, name_source='in_file', name_template='%s_masked'), clfrac=dict(argstr='-clfrac %s'), dilate=dict(argstr='-dilate %s'), environ=dict(nohash=True, usedefault=True), erode=dict(argstr='-erode %s'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_mask'), outputtype=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), brain_file=dict(argstr='-apply_prefix %s', extensions=None, name_source='in_file', name_template='%s_masked'), clfrac=dict(argstr='-clfrac %s'), dilate=dict(argstr='-dilate %s'), environ=dict(nohash=True, usedefault=True), erode=dict(argstr='-erode %s'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_mask'), outputtype=dict())
```

## Next Steps


---

*Source: test_auto_Automask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*