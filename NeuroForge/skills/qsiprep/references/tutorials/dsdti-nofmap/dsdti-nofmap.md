# How To: Dsdti Nofmap

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: DSCDTI_nofmap test.

Was in DSDTI_nofmap.sh.

This tests the following features:
- A workflow with no distortion correction followed by eddy
- Eddy is run on a CPU
- Denoising is skipped

Inputs
------
- DSDTI BIDS data (data/DSDTI)

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

### Step 1: 'DSCDTI_nofmap test.\n\n    Was in DSDTI_nofmap.sh.\n\n    This tests the following features:\n    - A workflow with no distortion correction followed by eddy\n    - Eddy is run on a CPU\n    - Denoising is skipped\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/DSDTI)\n    '

```python
'DSCDTI_nofmap test.\n\n    Was in DSDTI_nofmap.sh.\n\n    This tests the following features:\n    - A workflow with no distortion correction followed by eddy\n    - Eddy is run on a CPU\n    - Denoising is skipped\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/DSDTI)\n    '
```

### Step 2: Assign TEST_NAME = 'dsdti_nofmap'

```python
TEST_NAME = 'dsdti_nofmap'
```

### Step 3: Assign dataset_dir = download_test_data(...)

```python
dataset_dir = download_test_data('DSDTI', data_dir)
```

### Step 4: Assign dataset_dir = os.path.join(...)

```python
dataset_dir = os.path.join(dataset_dir, 'DSDTI')
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
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', f'--eddy-config={eddy_config}', '--denoise-method=none', '--unringing-method=rpg', '--b1-biascorrect-stage=none', '--output-resolution=5']
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
'DSCDTI_nofmap test.\n\n    Was in DSDTI_nofmap.sh.\n\n    This tests the following features:\n    - A workflow with no distortion correction followed by eddy\n    - Eddy is run on a CPU\n    - Denoising is skipped\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/DSDTI)\n    '
TEST_NAME = 'dsdti_nofmap'
dataset_dir = download_test_data('DSDTI', data_dir)
dataset_dir = os.path.join(dataset_dir, 'DSDTI')
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
test_data_path = get_test_data_path()
eddy_config = os.path.join(test_data_path, 'eddy_config.json')
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', f'--eddy-config={eddy_config}', '--denoise-method=none', '--unringing-method=rpg', '--b1-biascorrect-stage=none', '--output-resolution=5']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

## Next Steps


---

*Source: test_cli.py:323 | Complexity: Advanced | Last updated: 2026-05-18*