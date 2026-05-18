# How To: Slicetiming Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SliceTiming inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(in_files=dict(copyfile=False, field='scans', mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), num_slices=dict(field='nslices', mandatory=True), out_prefix=dict(field='prefix', usedefault=True), paths=dict(), ref_slice=dict(field='refslice', mandatory=True), slice_order=dict(field='so', mandatory=True), time_acquisition=dict(field='ta', mandatory=True), time_repetition=dict(field='tr', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(in_files=dict(copyfile=False, field='scans', mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), num_slices=dict(field='nslices', mandatory=True), out_prefix=dict(field='prefix', usedefault=True), paths=dict(), ref_slice=dict(field='refslice', mandatory=True), slice_order=dict(field='so', mandatory=True), time_acquisition=dict(field='ta', mandatory=True), time_repetition=dict(field='tr', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_SliceTiming.py:6 | Complexity: Beginner | Last updated: 2026-05-18*