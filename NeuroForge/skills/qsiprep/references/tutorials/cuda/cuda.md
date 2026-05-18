# How To: Cuda

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Was in CUDATest.sh.
XXX: Not called in CircleCI.

This tests the following features:
- Blip-up + Blip-down DWI series for TOPUP/Eddy
- Eddy is run on a CPU
- Denoising is skipped

Inputs
------
- DSDTI BIDS data (data/drbuddi_rpe_series)

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

### Step 1: '\n\n    Was in CUDATest.sh.\n    XXX: Not called in CircleCI.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - Denoising is skipped\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/drbuddi_rpe_series)\n    '

```python
'\n\n    Was in CUDATest.sh.\n    XXX: Not called in CircleCI.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - Denoising is skipped\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/drbuddi_rpe_series)\n    '
```

### Step 2: Assign TEST_NAME = 'cuda'

```python
TEST_NAME = 'cuda'
```

### Step 3: Assign dataset_dir = download_test_data(...)

```python
dataset_dir = download_test_data('drbuddi_rpe_series', data_dir)
```

### Step 4: Assign dataset_dir = os.path.join(...)

```python
dataset_dir = os.path.join(dataset_dir, 'qsiprep')
```

### Step 5: Assign out_dir = os.path.join(...)

```python
out_dir = os.path.join(output_dir, TEST_NAME)
```

### Step 6: Assign work_dir = os.path.join(...)

```python
work_dir = os.path.join(working_dir, TEST_NAME)
```

### Step 7: Assign test_data_path = get_test_data_path(...)

```python
test_data_path = get_test_data_path()
```

### Step 8: Assign eddy_config = os.path.join(...)

```python
eddy_config = os.path.join(test_data_path, 'eddy_config.json')
```

### Step 9: Assign parameters = value

```python
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--anat-modality=none', '--denoise-method=none', '--b1-biascorrect-stage=none', '--pepolar-method=DRBUDDI', f'--eddy-config={eddy_config}', '--output-resolution=5']
```

### Step 10: Call _run_and_generate()

```python
_run_and_generate(TEST_NAME, parameters, test_main=False)
```


## Complete Example

```python
# Setup
# Fixtures: data_dir, output_dir, working_dir

# Workflow
'\n\n    Was in CUDATest.sh.\n    XXX: Not called in CircleCI.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - Denoising is skipped\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/drbuddi_rpe_series)\n    '
TEST_NAME = 'cuda'
dataset_dir = download_test_data('drbuddi_rpe_series', data_dir)
dataset_dir = os.path.join(dataset_dir, 'qsiprep')
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
test_data_path = get_test_data_path()
eddy_config = os.path.join(test_data_path, 'eddy_config.json')
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--anat-modality=none', '--denoise-method=none', '--b1-biascorrect-stage=none', '--pepolar-method=DRBUDDI', f'--eddy-config={eddy_config}', '--output-resolution=5']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

## Next Steps


---

*Source: test_cli.py:113 | Complexity: Advanced | Last updated: 2026-05-18*