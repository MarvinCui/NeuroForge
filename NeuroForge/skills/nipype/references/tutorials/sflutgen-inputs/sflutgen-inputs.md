# How To: Sflutgen Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SFLUTGen inputs

## Prerequisites

**Required Modules:**
- `calib`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), binincsize=dict(argstr='-binincsize %d', units='NA'), directmap=dict(argstr='-directmap'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True), info_file=dict(argstr='-infofile %s', extensions=None, mandatory=True), minvectsperbin=dict(argstr='-minvectsperbin %d', units='NA'), order=dict(argstr='-order %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outputstem=dict(argstr='-outputstem %s', usedefault=True), pdf=dict(argstr='-pdf %s', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), binincsize=dict(argstr='-binincsize %d', units='NA'), directmap=dict(argstr='-directmap'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True), info_file=dict(argstr='-infofile %s', extensions=None, mandatory=True), minvectsperbin=dict(argstr='-minvectsperbin %d', units='NA'), order=dict(argstr='-order %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outputstem=dict(argstr='-outputstem %s', usedefault=True), pdf=dict(argstr='-pdf %s', usedefault=True))
```

## Next Steps


---

*Source: test_auto_SFLUTGen.py:6 | Complexity: Beginner | Last updated: 2026-05-18*