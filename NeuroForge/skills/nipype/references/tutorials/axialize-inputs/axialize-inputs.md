# How To: Axialize Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Axialize inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), axial=dict(argstr='-axial', xor=['coronal', 'sagittal']), coronal=dict(argstr='-coronal', xor=['sagittal', 'axial']), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-2), num_threads=dict(nohash=True, usedefault=True), orientation=dict(argstr='-orient %s'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_axialize'), outputtype=dict(), sagittal=dict(argstr='-sagittal', xor=['coronal', 'axial']), verb=dict(argstr='-verb'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), axial=dict(argstr='-axial', xor=['coronal', 'sagittal']), coronal=dict(argstr='-coronal', xor=['sagittal', 'axial']), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-2), num_threads=dict(nohash=True, usedefault=True), orientation=dict(argstr='-orient %s'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_axialize'), outputtype=dict(), sagittal=dict(argstr='-sagittal', xor=['coronal', 'axial']), verb=dict(argstr='-verb'))
```

## Next Steps


---

*Source: test_auto_Axialize.py:6 | Complexity: Beginner | Last updated: 2026-05-18*