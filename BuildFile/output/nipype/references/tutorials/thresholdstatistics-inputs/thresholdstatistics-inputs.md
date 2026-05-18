# How To: Thresholdstatistics Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ThresholdStatistics inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(contrast_index=dict(mandatory=True), extent_threshold=dict(usedefault=True), height_threshold=dict(mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), spm_mat_file=dict(copyfile=True, extensions=None, mandatory=True), stat_image=dict(copyfile=False, extensions=None, mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(contrast_index=dict(mandatory=True), extent_threshold=dict(usedefault=True), height_threshold=dict(mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), spm_mat_file=dict(copyfile=True, extensions=None, mandatory=True), stat_image=dict(copyfile=False, extensions=None, mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_ThresholdStatistics.py:6 | Complexity: Beginner | Last updated: 2026-05-18*