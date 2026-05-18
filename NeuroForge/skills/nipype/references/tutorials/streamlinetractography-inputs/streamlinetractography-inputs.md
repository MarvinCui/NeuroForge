# How To: Streamlinetractography Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test StreamlineTractography inputs

## Prerequisites

**Required Modules:**
- `tracks`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(gfa_thresh=dict(mandatory=True, usedefault=True), in_file=dict(extensions=None, mandatory=True), in_model=dict(extensions=None), in_peaks=dict(extensions=None), min_angle=dict(mandatory=True, usedefault=True), multiprocess=dict(mandatory=True, usedefault=True), num_seeds=dict(mandatory=True, usedefault=True), out_prefix=dict(), peak_threshold=dict(mandatory=True, usedefault=True), save_seeds=dict(mandatory=True, usedefault=True), seed_coord=dict(extensions=None), seed_mask=dict(extensions=None), tracking_mask=dict(extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(gfa_thresh=dict(mandatory=True, usedefault=True), in_file=dict(extensions=None, mandatory=True), in_model=dict(extensions=None), in_peaks=dict(extensions=None), min_angle=dict(mandatory=True, usedefault=True), multiprocess=dict(mandatory=True, usedefault=True), num_seeds=dict(mandatory=True, usedefault=True), out_prefix=dict(), peak_threshold=dict(mandatory=True, usedefault=True), save_seeds=dict(mandatory=True, usedefault=True), seed_coord=dict(extensions=None), seed_mask=dict(extensions=None), tracking_mask=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_StreamlineTractography.py:6 | Complexity: Beginner | Last updated: 2026-05-18*