# How To: First Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FIRST inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(affine_file=dict(argstr='-a %s', extensions=None, position=6), args=dict(argstr='%s'), brain_extracted=dict(argstr='-b', position=2), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', copyfile=False, extensions=None, mandatory=True, position=-2), list_of_specific_structures=dict(argstr='-s %s', position=5, sep=','), method=dict(argstr='-m %s', position=4, usedefault=True, xor=['method_as_numerical_threshold']), method_as_numerical_threshold=dict(argstr='-m %.4f', position=4), no_cleanup=dict(argstr='-d', position=3), out_file=dict(argstr='-o %s', extensions=None, hash_files=False, mandatory=True, position=-1, usedefault=True), output_type=dict(), verbose=dict(argstr='-v', position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(affine_file=dict(argstr='-a %s', extensions=None, position=6), args=dict(argstr='%s'), brain_extracted=dict(argstr='-b', position=2), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', copyfile=False, extensions=None, mandatory=True, position=-2), list_of_specific_structures=dict(argstr='-s %s', position=5, sep=','), method=dict(argstr='-m %s', position=4, usedefault=True, xor=['method_as_numerical_threshold']), method_as_numerical_threshold=dict(argstr='-m %.4f', position=4), no_cleanup=dict(argstr='-d', position=3), out_file=dict(argstr='-o %s', extensions=None, hash_files=False, mandatory=True, position=-1, usedefault=True), output_type=dict(), verbose=dict(argstr='-v', position=1))
```

## Next Steps


---

*Source: test_auto_FIRST.py:6 | Complexity: Beginner | Last updated: 2026-05-18*