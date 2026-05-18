# How To: Autotcorrelate Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AutoTcorrelate inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), eta2=dict(argstr='-eta2'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None), mask_only_targets=dict(argstr='-mask_only_targets', xor=['mask_source']), mask_source=dict(argstr='-mask_source %s', extensions=None, xor=['mask_only_targets']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_similarity_matrix.1D'), outputtype=dict(), polort=dict(argstr='-polort %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), eta2=dict(argstr='-eta2'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None), mask_only_targets=dict(argstr='-mask_only_targets', xor=['mask_source']), mask_source=dict(argstr='-mask_source %s', extensions=None, xor=['mask_only_targets']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_similarity_matrix.1D'), outputtype=dict(), polort=dict(argstr='-polort %d'))
```

## Next Steps


---

*Source: test_auto_AutoTcorrelate.py:6 | Complexity: Beginner | Last updated: 2026-05-18*