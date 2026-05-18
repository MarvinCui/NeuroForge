# How To: Dscsdsi Fmap

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Run AllFieldmaps test on DSCSDSI data.

Was in AllFieldmapsTests.sh. I split it between this and the DSDTI test.
XXX: Not called in CircleCI.

Instead of running full workflows, this test checks that workflows can
be built for all sorts of fieldmap configurations.

This tests the following features:
- Blip-up + Blip-down DWI series for TOPUP/Eddy
- Eddy is run on a CPU
- dwidenoise is enabled explicitly

Inputs
------
- DSDTI BIDS data (data/DSCSDSI_fmap)

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

### Step 1: 'Run AllFieldmaps test on DSCSDSI data.\n\n    Was in AllFieldmapsTests.sh. I split it between this and the DSDTI test.\n    XXX: Not called in CircleCI.\n\n    Instead of running full workflows, this test checks that workflows can\n    be built for all sorts of fieldmap configurations.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - dwidenoise is enabled explicitly\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/DSCSDSI_fmap)\n    '

```python
'Run AllFieldmaps test on DSCSDSI data.\n\n    Was in AllFieldmapsTests.sh. I split it between this and the DSDTI test.\n    XXX: Not called in CircleCI.\n\n    Instead of running full workflows, this test checks that workflows can\n    be built for all sorts of fieldmap configurations.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - dwidenoise is enabled explicitly\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/DSCSDSI_fmap)\n    '
```

### Step 2: Assign TEST_NAME = 'dscsdsi_fmap'

```python
TEST_NAME = 'dscsdsi_fmap'
```

### Step 3: Assign dataset_dir = download_test_data(...)

```python
dataset_dir = download_test_data('DSCSDSI_fmap', data_dir)
```

### Step 4: Assign out_dir = os.path.join(...)

```python
out_dir = os.path.join(output_dir, TEST_NAME)
```

### Step 5: Assign work_dir = os.path.join(...)

```python
work_dir = os.path.join(working_dir, TEST_NAME)
```

### Step 6: Assign parameters = value

```python
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--boilerplate', '--sloppy', '--denoise-method=dwidenoise', '--b0-motion-corr-to=first', '--write-graph', '--mem-mb=4096', '--output-resolution=5']
```

### Step 7: Call _run_and_generate()

```python
_run_and_generate(TEST_NAME, parameters, test_main=False)
```


## Complete Example

```python
# Setup
# Fixtures: data_dir, output_dir, working_dir

# Workflow
'Run AllFieldmaps test on DSCSDSI data.\n\n    Was in AllFieldmapsTests.sh. I split it between this and the DSDTI test.\n    XXX: Not called in CircleCI.\n\n    Instead of running full workflows, this test checks that workflows can\n    be built for all sorts of fieldmap configurations.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - dwidenoise is enabled explicitly\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/DSCSDSI_fmap)\n    '
TEST_NAME = 'dscsdsi_fmap'
dataset_dir = download_test_data('DSCSDSI_fmap', data_dir)
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--boilerplate', '--sloppy', '--denoise-method=dwidenoise', '--b0-motion-corr-to=first', '--write-graph', '--mem-mb=4096', '--output-resolution=5']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

## Next Steps


---

*Source: test_cli.py:70 | Complexity: Intermediate | Last updated: 2026-05-18*