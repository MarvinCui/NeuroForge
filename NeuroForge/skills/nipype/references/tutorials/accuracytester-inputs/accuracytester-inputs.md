# How To: Accuracytester Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AccuracyTester inputs

## Prerequisites

**Required Modules:**
- `fix`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), mel_icas=dict(argstr='%s', copyfile=False, mandatory=True, position=3), output_directory=dict(argstr='%s', mandatory=True, position=2), trained_wts_file=dict(argstr='%s', extensions=None, mandatory=True, position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), mel_icas=dict(argstr='%s', copyfile=False, mandatory=True, position=3), output_directory=dict(argstr='%s', mandatory=True, position=2), trained_wts_file=dict(argstr='%s', extensions=None, mandatory=True, position=1))
```

## Next Steps


---

*Source: test_auto_AccuracyTester.py:6 | Complexity: Beginner | Last updated: 2026-05-18*