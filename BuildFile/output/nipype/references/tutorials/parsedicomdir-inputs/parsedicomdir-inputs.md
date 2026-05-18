# How To: Parsedicomdir Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ParseDICOMDir inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dicom_dir=dict(argstr='--d %s', mandatory=True), dicom_info_file=dict(argstr='--o %s', extensions=None, usedefault=True), environ=dict(nohash=True, usedefault=True), sortbyrun=dict(argstr='--sortbyrun'), subjects_dir=dict(), summarize=dict(argstr='--summarize'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dicom_dir=dict(argstr='--d %s', mandatory=True), dicom_info_file=dict(argstr='--o %s', extensions=None, usedefault=True), environ=dict(nohash=True, usedefault=True), sortbyrun=dict(argstr='--sortbyrun'), subjects_dir=dict(), summarize=dict(argstr='--summarize'))
```

## Next Steps


---

*Source: test_auto_ParseDICOMDir.py:6 | Complexity: Beginner | Last updated: 2026-05-18*