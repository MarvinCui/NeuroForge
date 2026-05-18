# How To: Afnitonifti Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AFNItoNIFTI inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), denote=dict(argstr='-denote'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), newid=dict(argstr='-newid', xor=['oldid']), num_threads=dict(nohash=True, usedefault=True), oldid=dict(argstr='-oldid', xor=['newid']), out_file=dict(argstr='-prefix %s', extensions=None, hash_files=False, name_source='in_file', name_template='%s.nii'), outputtype=dict(), pure=dict(argstr='-pure'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), denote=dict(argstr='-denote'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), newid=dict(argstr='-newid', xor=['oldid']), num_threads=dict(nohash=True, usedefault=True), oldid=dict(argstr='-oldid', xor=['newid']), out_file=dict(argstr='-prefix %s', extensions=None, hash_files=False, name_source='in_file', name_template='%s.nii'), outputtype=dict(), pure=dict(argstr='-pure'))
```

## Next Steps


---

*Source: test_auto_AFNItoNIFTI.py:6 | Complexity: Beginner | Last updated: 2026-05-18*