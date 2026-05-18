# How To: Dicomconvert Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DICOMConvert inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), base_output_dir=dict(mandatory=True), dicom_dir=dict(mandatory=True), dicom_info=dict(extensions=None), environ=dict(nohash=True, usedefault=True), file_mapping=dict(), ignore_single_slice=dict(requires=['dicom_info']), out_type=dict(usedefault=True), seq_list=dict(requires=['dicom_info']), subject_dir_template=dict(usedefault=True), subject_id=dict(), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), base_output_dir=dict(mandatory=True), dicom_dir=dict(mandatory=True), dicom_info=dict(extensions=None), environ=dict(nohash=True, usedefault=True), file_mapping=dict(), ignore_single_slice=dict(requires=['dicom_info']), out_type=dict(usedefault=True), seq_list=dict(requires=['dicom_info']), subject_dir_template=dict(usedefault=True), subject_id=dict(), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_DICOMConvert.py:6 | Complexity: Beginner | Last updated: 2026-05-18*