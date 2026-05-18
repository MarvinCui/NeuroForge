# How To: Classifier Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Classifier inputs

## Prerequisites

**Required Modules:**
- `fix`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), artifacts_list_file=dict(extensions=None), environ=dict(nohash=True, usedefault=True), mel_ica=dict(argstr='%s', copyfile=False, position=1), thresh=dict(argstr='%d', mandatory=True, position=-1), trained_wts_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), artifacts_list_file=dict(extensions=None), environ=dict(nohash=True, usedefault=True), mel_ica=dict(argstr='%s', copyfile=False, position=1), thresh=dict(argstr='%d', mandatory=True, position=-1), trained_wts_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=2))
```

## Next Steps


---

*Source: test_auto_Classifier.py:6 | Complexity: Beginner | Last updated: 2026-05-18*