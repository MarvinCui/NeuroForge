# How To: Fitglm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FitGLM inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(TR=dict(mandatory=True), drift_model=dict(usedefault=True), hrf_model=dict(usedefault=True), mask=dict(extensions=None), method=dict(usedefault=True), model=dict(usedefault=True), normalize_design_matrix=dict(usedefault=True), plot_design_matrix=dict(usedefault=True), save_residuals=dict(usedefault=True), session_info=dict(mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(TR=dict(mandatory=True), drift_model=dict(usedefault=True), hrf_model=dict(usedefault=True), mask=dict(extensions=None), method=dict(usedefault=True), model=dict(usedefault=True), normalize_design_matrix=dict(usedefault=True), plot_design_matrix=dict(usedefault=True), save_residuals=dict(usedefault=True), session_info=dict(mandatory=True))
```

## Next Steps


---

*Source: test_auto_FitGLM.py:6 | Complexity: Beginner | Last updated: 2026-05-18*