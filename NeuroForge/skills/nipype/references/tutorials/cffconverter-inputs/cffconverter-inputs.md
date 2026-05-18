# How To: Cffconverter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CFFConverter inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(creator=dict(), data_files=dict(), description=dict(usedefault=True), email=dict(), gifti_labels=dict(), gifti_surfaces=dict(), gpickled_networks=dict(), graphml_networks=dict(), license=dict(), nifti_volumes=dict(), out_file=dict(extensions=None, usedefault=True), publisher=dict(), references=dict(), relation=dict(), rights=dict(), script_files=dict(), species=dict(usedefault=True), timeseries_files=dict(), title=dict(), tract_files=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(creator=dict(), data_files=dict(), description=dict(usedefault=True), email=dict(), gifti_labels=dict(), gifti_surfaces=dict(), gpickled_networks=dict(), graphml_networks=dict(), license=dict(), nifti_volumes=dict(), out_file=dict(extensions=None, usedefault=True), publisher=dict(), references=dict(), relation=dict(), rights=dict(), script_files=dict(), species=dict(usedefault=True), timeseries_files=dict(), title=dict(), tract_files=dict())
```

## Next Steps


---

*Source: test_auto_CFFConverter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*