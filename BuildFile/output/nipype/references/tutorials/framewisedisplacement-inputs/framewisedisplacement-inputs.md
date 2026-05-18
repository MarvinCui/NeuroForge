# How To: Framewisedisplacement Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FramewiseDisplacement inputs

## Prerequisites

**Required Modules:**
- `confounds`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(figdpi=dict(usedefault=True), figsize=dict(usedefault=True), in_file=dict(extensions=None, mandatory=True), normalize=dict(usedefault=True), out_figure=dict(extensions=None, usedefault=True), out_file=dict(extensions=None, usedefault=True), parameter_source=dict(mandatory=True), radius=dict(usedefault=True), save_plot=dict(usedefault=True), series_tr=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(figdpi=dict(usedefault=True), figsize=dict(usedefault=True), in_file=dict(extensions=None, mandatory=True), normalize=dict(usedefault=True), out_figure=dict(extensions=None, usedefault=True), out_file=dict(extensions=None, usedefault=True), parameter_source=dict(mandatory=True), radius=dict(usedefault=True), save_plot=dict(usedefault=True), series_tr=dict())
```

## Next Steps


---

*Source: test_auto_FramewiseDisplacement.py:6 | Complexity: Beginner | Last updated: 2026-05-18*