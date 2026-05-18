# How To: Dicomimport Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DicomImport inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(format=dict(field='convopts.format', usedefault=True), icedims=dict(field='convopts.icedims', usedefault=True), in_files=dict(field='data', mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), output_dir=dict(field='outdir', usedefault=True), output_dir_struct=dict(field='root', usedefault=True), paths=dict(), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(format=dict(field='convopts.format', usedefault=True), icedims=dict(field='convopts.icedims', usedefault=True), in_files=dict(field='data', mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), output_dir=dict(field='outdir', usedefault=True), output_dir_struct=dict(field='root', usedefault=True), paths=dict(), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_DicomImport.py:6 | Complexity: Beginner | Last updated: 2026-05-18*