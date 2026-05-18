# How To: Gennlxfm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Gennlxfm inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), ident=dict(argstr='-ident'), like=dict(argstr='-like %s', extensions=None), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['like'], name_template='%s_gennlxfm.xfm', position=-1), step=dict(argstr='-step %s'), verbose=dict(argstr='-verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), ident=dict(argstr='-ident'), like=dict(argstr='-like %s', extensions=None), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['like'], name_template='%s_gennlxfm.xfm', position=-1), step=dict(argstr='-step %s'), verbose=dict(argstr='-verbose'))
```

## Next Steps


---

*Source: test_auto_Gennlxfm.py:6 | Complexity: Beginner | Last updated: 2026-05-18*