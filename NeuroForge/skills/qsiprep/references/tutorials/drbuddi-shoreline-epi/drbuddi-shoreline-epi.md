# How To: Drbuddi Shoreline Epi

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test EPI fieldmap correction with SHORELine + DRBUDDI.

Was in DRBUDDI_SHORELine_epi.sh.

This tests the following features:
- SHORELine (here, just b=0 registration) motion correction

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

### Step 1: 'Test EPI fieldmap correction with SHORELine + DRBUDDI.\n\n    Was in DRBUDDI_SHORELine_epi.sh.\n\n    This tests the following features:\n    - SHORELine (here, just b=0 registration) motion correction\n    '

```python
'Test EPI fieldmap correction with SHORELine + DRBUDDI.\n\n    Was in DRBUDDI_SHORELine_epi.sh.\n\n    This tests the following features:\n    - SHORELine (here, just b=0 registration) motion correction\n    '
```

### Step 2: Assign TEST_NAME = 'drbuddi_shoreline_epi'

```python
TEST_NAME = 'drbuddi_shoreline_epi'
```

### Step 3: Assign dataset_dir = download_test_data(...)

```python
dataset_dir = download_test_data('drbuddi_epi', data_dir)
```

### Step 4: Assign dataset_dir = os.path.join(...)

```python
dataset_dir = os.path.join(dataset_dir, 'tinytensor_epi')
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
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--anat-modality=none', '--denoise-method=none', '--b0-motion-corr-to=first', '--b1-biascorrect-stage=none', '--pepolar-method=DRBUDDI', '--hmc-model=none', '--output-resolution=2', '--shoreline-iters=1']
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
'Test EPI fieldmap correction with SHORELine + DRBUDDI.\n\n    Was in DRBUDDI_SHORELine_epi.sh.\n\n    This tests the following features:\n    - SHORELine (here, just b=0 registration) motion correction\n    '
TEST_NAME = 'drbuddi_shoreline_epi'
dataset_dir = download_test_data('drbuddi_epi', data_dir)
dataset_dir = os.path.join(dataset_dir, 'tinytensor_epi')
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--anat-modality=none', '--denoise-method=none', '--b0-motion-corr-to=first', '--b1-biascorrect-stage=none', '--pepolar-method=DRBUDDI', '--hmc-model=none', '--output-resolution=2', '--shoreline-iters=1']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

## Next Steps


---

*Source: test_cli.py:203 | Complexity: Advanced | Last updated: 2026-05-18*