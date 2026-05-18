# How To: Dscsdsi

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: DSCSDSI test

Was in DSCSDSI.sh.

This tests the following features:
- Whether the --anat-only workflow is successful
- Whether the regular qsiprep workflow can resume using the working directory from --anat-only
- The SHORELine motion correction workflow
- Skipping B1 biascorrection
- Using the SyN-SDC distortion correction method
- dwidenoise is enabled implicitly

Inputs
------
- DSCSDSI BIDS data (data/DSCSDSI_nofmap)

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

### Step 1: 'DSCSDSI test\n\n    Was in DSCSDSI.sh.\n\n    This tests the following features:\n    - Whether the --anat-only workflow is successful\n    - Whether the regular qsiprep workflow can resume using the working directory from --anat-only\n    - The SHORELine motion correction workflow\n    - Skipping B1 biascorrection\n    - Using the SyN-SDC distortion correction method\n    - dwidenoise is enabled implicitly\n\n    Inputs\n    ------\n    - DSCSDSI BIDS data (data/DSCSDSI_nofmap)\n    '

```python
'DSCSDSI test\n\n    Was in DSCSDSI.sh.\n\n    This tests the following features:\n    - Whether the --anat-only workflow is successful\n    - Whether the regular qsiprep workflow can resume using the working directory from --anat-only\n    - The SHORELine motion correction workflow\n    - Skipping B1 biascorrection\n    - Using the SyN-SDC distortion correction method\n    - dwidenoise is enabled implicitly\n\n    Inputs\n    ------\n    - DSCSDSI BIDS data (data/DSCSDSI_nofmap)\n    '
```

### Step 2: Assign TEST_NAME = 'dscsdsi'

```python
TEST_NAME = 'dscsdsi'
```

### Step 3: Assign dataset_dir = download_test_data(...)

```python
dataset_dir = download_test_data('DSCSDSI', data_dir)
```

### Step 4: Assign dataset_dir = os.path.join(...)

```python
dataset_dir = os.path.join(dataset_dir, 'DSCSDSI_nofmap')
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
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--write-graph', '--use-syn-sdc', '--force-syn', '--b1-biascorrect-stage=none', '--hmc-model=3dSHORE', '--hmc-transform=Rigid', '--output-resolution=5', '--shoreline-iters=1']
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
'DSCSDSI test\n\n    Was in DSCSDSI.sh.\n\n    This tests the following features:\n    - Whether the --anat-only workflow is successful\n    - Whether the regular qsiprep workflow can resume using the working directory from --anat-only\n    - The SHORELine motion correction workflow\n    - Skipping B1 biascorrection\n    - Using the SyN-SDC distortion correction method\n    - dwidenoise is enabled implicitly\n\n    Inputs\n    ------\n    - DSCSDSI BIDS data (data/DSCSDSI_nofmap)\n    '
TEST_NAME = 'dscsdsi'
dataset_dir = download_test_data('DSCSDSI', data_dir)
dataset_dir = os.path.join(dataset_dir, 'DSCSDSI_nofmap')
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--write-graph', '--use-syn-sdc', '--force-syn', '--b1-biascorrect-stage=none', '--hmc-model=3dSHORE', '--hmc-transform=Rigid', '--output-resolution=5', '--shoreline-iters=1']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

## Next Steps


---

*Source: test_cli.py:277 | Complexity: Advanced | Last updated: 2026-05-18*