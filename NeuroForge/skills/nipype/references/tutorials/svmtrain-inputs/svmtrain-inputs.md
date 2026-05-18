# How To: Svmtrain Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SVMTrain inputs

## Prerequisites

**Required Modules:**
- `svm`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(alphas=dict(argstr='-alpha %s', extensions=None, name_source='in_file', name_template='%s_alphas', suffix='_alphas'), args=dict(argstr='%s'), censor=dict(argstr='-censor %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-trainvol %s', copyfile=False, extensions=None, mandatory=True), kernel=dict(argstr='-kernel %s'), mask=dict(argstr='-mask %s', copyfile=False, extensions=None, position=-1), max_iterations=dict(argstr='-max_iterations %d'), model=dict(argstr='-model %s', extensions=None, name_source='in_file', name_template='%s_model', suffix='_model'), nomodelmask=dict(argstr='-nomodelmask'), num_threads=dict(nohash=True, usedefault=True), options=dict(argstr='%s'), out_file=dict(argstr='-bucket %s', extensions=None, name_source='in_file', name_template='%s_vectors', suffix='_bucket'), outputtype=dict(), trainlabels=dict(argstr='-trainlabels %s', extensions=None), ttype=dict(argstr='-type %s', mandatory=True), w_out=dict(argstr='-wout'))
```


## Complete Example

```python
# Workflow
input_map = dict(alphas=dict(argstr='-alpha %s', extensions=None, name_source='in_file', name_template='%s_alphas', suffix='_alphas'), args=dict(argstr='%s'), censor=dict(argstr='-censor %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-trainvol %s', copyfile=False, extensions=None, mandatory=True), kernel=dict(argstr='-kernel %s'), mask=dict(argstr='-mask %s', copyfile=False, extensions=None, position=-1), max_iterations=dict(argstr='-max_iterations %d'), model=dict(argstr='-model %s', extensions=None, name_source='in_file', name_template='%s_model', suffix='_model'), nomodelmask=dict(argstr='-nomodelmask'), num_threads=dict(nohash=True, usedefault=True), options=dict(argstr='%s'), out_file=dict(argstr='-bucket %s', extensions=None, name_source='in_file', name_template='%s_vectors', suffix='_bucket'), outputtype=dict(), trainlabels=dict(argstr='-trainlabels %s', extensions=None), ttype=dict(argstr='-type %s', mandatory=True), w_out=dict(argstr='-wout'))
```

## Next Steps


---

*Source: test_auto_SVMTrain.py:6 | Complexity: Beginner | Last updated: 2026-05-18*