# How To: Intramodal Template

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: IntramodalTemplate test

A two-session dataset is used to create an intramodal template.

This tests the following features:
- Blip-up + Blip-down DWI series for TOPUP/Eddy
- Eddy is run on a CPU
- dwidenoise is enabled implicitly

Inputs
------
- twoses BIDS data (data/DSDTI_fmap)

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `sys`
- `pathlib`
- `unittest.mock`
- `nibabel`
- `numpy`
- `pytest`
- `nipype`
- `qsiprep.cli`
- `qsiprep.cli.parser`
- `qsiprep.cli.workflow`
- `qsiprep.reports.core`
- `qsiprep.tests.utils`
- `qsiprep.utils.bids`
- `qsiprep`

**Setup Required:**
```python
# Fixtures: data_dir, output_dir, working_dir
```

## Step-by-Step Guide

### Step 1: 'IntramodalTemplate test\n\n    A two-session dataset is used to create an intramodal template.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - dwidenoise is enabled implicitly\n\n    Inputs\n    ------\n    - twoses BIDS data (data/DSDTI_fmap)\n    '

```python
'IntramodalTemplate test\n\n    A two-session dataset is used to create an intramodal template.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - dwidenoise is enabled implicitly\n\n    Inputs\n    ------\n    - twoses BIDS data (data/DSDTI_fmap)\n    '
```

### Step 2: Assign TEST_NAME = 'intramodal_template'

```python
TEST_NAME = 'intramodal_template'
```

### Step 3: Assign dataset_dir = download_test_data(...)

```python
dataset_dir = download_test_data('twoses', data_dir)
```

### Step 4: Assign dataset_dir = os.path.join(...)

```python
dataset_dir = os.path.join(dataset_dir, 'twoses')
```

### Step 5: Assign out_dir = os.path.join(...)

```python
out_dir = os.path.join(output_dir, TEST_NAME)
```

### Step 6: Assign work_dir = os.path.join(...)

```python
work_dir = os.path.join(working_dir, TEST_NAME)
```

### Step 7: Assign parameters = value

```python
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--b1-biascorrect-stage=none', '--hmc-model=none', '--b0-motion-corr-to=first', '--output-resolution=5', '--intramodal-template-transform=BSplineSyN', '--intramodal-template-iters=2']
```

### Step 8: Call _run_and_generate()

```python
_run_and_generate(TEST_NAME, parameters, test_main=False)
```


## Complete Example

```python
# Setup
# Fixtures: data_dir, output_dir, working_dir

# Workflow
'IntramodalTemplate test\n\n    A two-session dataset is used to create an intramodal template.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - dwidenoise is enabled implicitly\n\n    Inputs\n    ------\n    - twoses BIDS data (data/DSDTI_fmap)\n    '
TEST_NAME = 'intramodal_template'
dataset_dir = download_test_data('twoses', data_dir)
dataset_dir = os.path.join(dataset_dir, 'twoses')
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--b1-biascorrect-stage=none', '--hmc-model=none', '--b0-motion-corr-to=first', '--output-resolution=5', '--intramodal-template-transform=BSplineSyN', '--intramodal-template-iters=2']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

## Next Steps


---

*Source: test_cli.py:407 | Complexity: Advanced | Last updated: 2026-05-18*