# How To: Svmtest Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SVMTest inputs

## Prerequisites

**Required Modules:**
- `svm`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), classout=dict(argstr='-classout'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-testvol %s', extensions=None, mandatory=True), model=dict(argstr='-model %s', mandatory=True), multiclass=dict(argstr='-multiclass %s'), nodetrend=dict(argstr='-nodetrend'), nopredcensord=dict(argstr='-nopredcensord'), num_threads=dict(nohash=True, usedefault=True), options=dict(argstr='%s'), out_file=dict(argstr='-predictions %s', extensions=None, name_template='%s_predictions'), outputtype=dict(), testlabels=dict(argstr='-testlabels %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), classout=dict(argstr='-classout'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-testvol %s', extensions=None, mandatory=True), model=dict(argstr='-model %s', mandatory=True), multiclass=dict(argstr='-multiclass %s'), nodetrend=dict(argstr='-nodetrend'), nopredcensord=dict(argstr='-nopredcensord'), num_threads=dict(nohash=True, usedefault=True), options=dict(argstr='%s'), out_file=dict(argstr='-predictions %s', extensions=None, name_template='%s_predictions'), outputtype=dict(), testlabels=dict(argstr='-testlabels %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_SVMTest.py:6 | Complexity: Beginner | Last updated: 2026-05-18*