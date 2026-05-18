---
name: qsiprep
description: Local codebase analysis for qsiprep
doc_version: 
---

# qsiprep Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `qsiprep`
**Files Analyzed:** 0
**Languages:** 
**Analysis Depth:** surface

## When to Use This Skill

Use this skill when you need to:
- Understand the codebase architecture and design patterns
- Find implementation examples and usage patterns
- Review API documentation extracted from code
- Check configuration patterns and best practices
- Explore test examples and real-world usage
- Navigate the codebase structure efficiently

## ⚡ Quick Reference

### Codebase Statistics

**Languages:**

**Analysis Performed:**
- ✅ API Reference (C2.5)
- ✅ Dependency Graph (C2.6)
- ✅ Design Patterns (C3.1)
- ✅ Test Examples (C3.2)
- ✅ Configuration Patterns (C3.4)
- ✅ Architectural Analysis (C3.7)
- ✅ Project Documentation (C3.9)

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Workflow: Test qsiprep.utils.bids.collect_data.** (complexity: 1.00)

```python
'Test qsiprep.utils.bids.collect_data.'
import pprint
from qsiprep.utils.bids import collect_data
bids_dir = tmpdir / name
generate_bids_skeleton(str(bids_dir), skeleton)
participant_label = '01'
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions[0], filters=None, bids_validate=False, ignore=[])[0]
assert len(subj_data['t1w']) == n_anats[0], pprint.pformat(subj_data)
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions[1], filters=None, bids_validate=False, ignore=[])[0]
assert len(subj_data['t1w']) == n_anats[1], pprint.pformat(subj_data)
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions, filters=None, bids_validate=False, ignore=['t2w'])[0]
assert len(subj_data['t1w']) == n_anats[2], pprint.pformat(subj_data)
assert len(subj_data['t2w']) == 0, pprint.pformat(subj_data)
```

**Workflow: Test qsiprep.interfaces.freesurfer.FixHeaderSynthStrip.** (complexity: 1.00)

```python
'Test qsiprep.interfaces.freesurfer.FixHeaderSynthStrip.'
tmpdir = tmp_path_factory.mktemp('test_synthstrip')
in_file = _resample_to_64_cube(_get_forrest_gump_t1w(datasets), tmpdir)
in_img = nb.load(in_file)
use_gpu = _gpu_available()
interface = freesurfer.FixHeaderSynthStrip(input_image=in_file, gpu=use_gpu)
results = interface.run(cwd=tmpdir)
assert os.path.isfile(results.outputs.out_brain)
assert os.path.isfile(results.outputs.out_brain_mask)
out_img = nb.load(results.outputs.out_brain)
mask_img = nb.load(results.outputs.out_brain_mask)
assert out_img.shape == in_img.shape
assert mask_img.shape == in_img.shape
```

**Workflow: Test qsiprep.interfaces.freesurfer.SynthSeg.** (complexity: 1.00)

```python
'Test qsiprep.interfaces.freesurfer.SynthSeg.'
tmpdir = tmp_path_factory.mktemp('test_synthseg')
in_file = _resample_to_64_cube(_get_forrest_gump_t1w(datasets), tmpdir)
use_gpu = _gpu_available()
interface = freesurfer.SynthSeg(input_image=in_file, cpu=not use_gpu)
results = interface.run(cwd=tmpdir)
assert os.path.isfile(results.outputs.out_seg)
assert os.path.isfile(results.outputs.out_post)
assert os.path.isfile(results.outputs.out_qc)
seg_img = nb.load(results.outputs.out_seg)
post_img = nb.load(results.outputs.out_post)
assert seg_img.shape == post_img.shape[:3]
```

**Workflow: Was in CUDATest.sh.
XXX: Not called in CircleCI.

This tests the following features:
- Blip-up + Blip-down DWI series for TOPUP/Eddy
- Eddy is run on a CPU
- Denoising is skipped

Inputs
------
- DSDTI BIDS data (data/drbuddi_rpe_series)** (complexity: 1.00)

```python
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

**Workflow: Was in DRBUDDI_eddy_rpe_series.sh.

This tests the following features:
- Blip-up + Blip-down DWI series for TOPUP/Eddy
- Eddy is run on a CPU
- Denoising is skipped

Inputs:
-------

- qsiprep single shell results (data/DSDTI_fmap)
- qsiprep multi shell results (data/DSDTI_fmap)** (complexity: 1.00)

```python
'\n\n    Was in DRBUDDI_eddy_rpe_series.sh.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - Denoising is skipped\n\n    Inputs:\n    -------\n\n    - qsiprep single shell results (data/DSDTI_fmap)\n    - qsiprep multi shell results (data/DSDTI_fmap)\n    '
TEST_NAME = 'drbuddi_rpe'
dataset_dir = download_test_data('drbuddi_rpe_series', data_dir)
dataset_dir = os.path.join(dataset_dir, 'tinytensor_rpe_series')
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
test_data_path = get_test_data_path()
eddy_config = os.path.join(test_data_path, 'eddy_config.json')
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', '--anat-modality=none', '--denoise-method=none', '--b0-motion-corr-to=first', '--b1-biascorrect-stage=none', '--pepolar-method=DRBUDDI', f'--eddy-config={eddy_config}', '--output-resolution=5']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

**Workflow: DSCDTI_nofmap test.

Was in DSDTI_nofmap.sh.

This tests the following features:
- A workflow with no distortion correction followed by eddy
- Eddy is run on a CPU
- Denoising is skipped

Inputs
------
- DSDTI BIDS data (data/DSDTI)** (complexity: 1.00)

```python
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

**Workflow: DSCDTI_synfmap test

Was in DSDTI_synfmap.sh.

This tests the following features:
- A workflow with no distortion correction followed by eddy
- Eddy is run on a CPU
- Denoising is skipped

Inputs
------
- DSDTI BIDS data (data/DSDTI)** (complexity: 1.00)

```python
'DSCDTI_synfmap test\n\n    Was in DSDTI_synfmap.sh.\n\n    This tests the following features:\n    - A workflow with no distortion correction followed by eddy\n    - Eddy is run on a CPU\n    - Denoising is skipped\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/DSDTI)\n    '
TEST_NAME = 'dsdti_synfmap'
dataset_dir = download_test_data('DSDTI', data_dir)
dataset_dir = os.path.join(dataset_dir, 'DSDTI')
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
test_data_path = get_test_data_path()
eddy_config = os.path.join(test_data_path, 'eddy_config.json')
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--sloppy', f'--eddy-config={eddy_config}', '--denoise-method=none', '--force-syn', '--b1-biascorrect-stage=final', '--output-resolution=5']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

**Workflow: Test qsiprep.interfaces.dipy.Patch2Self.** (complexity: 1.00)

```python
'Test qsiprep.interfaces.dipy.Patch2Self.'
tmpdir = tmp_path_factory.mktemp('test_patch2self')
in_dir = datasets['forrest_gump']
in_file = os.path.join(in_dir, 'sub-01/ses-forrestgump/dwi/sub-01_ses-forrestgump_dwi.nii.gz')
bval_file = os.path.join(in_dir, 'sub-01/ses-forrestgump/dwi/sub-01_ses-forrestgump_dwi.bval')
in_img = nb.load(in_file)
interface = dipy.Patch2Self(in_file=in_file, bval_file=bval_file)
results = interface.run(cwd=tmpdir)
assert os.path.isfile(results.outputs.out_file)
denoised_img = nb.load(results.outputs.out_file)
assert denoised_img.shape == in_img.shape
assert os.path.isfile(results.outputs.noise_image)
noise_img = nb.load(results.outputs.noise_image)
assert noise_img.shape == in_img.shape[:3]
assert noise_img.ndim == 3
assert os.path.isfile(results.outputs.out_report)
assert os.path.isfile(results.outputs.nmse_text)
```

**Workflow: Test qsiprep.interfaces.mrtrix.DWIDenoise.** (complexity: 1.00)

```python
'Test qsiprep.interfaces.mrtrix.DWIDenoise.'
tmpdir = tmp_path_factory.mktemp('test_dwidenoise')
in_dir = datasets['forrest_gump']
in_file = os.path.join(in_dir, 'sub-01/ses-forrestgump/dwi/sub-01_ses-forrestgump_dwi.nii.gz')
in_img = nb.load(in_file)
interface = mrtrix.DWIDenoise(extent=(5, 5, 5), in_file=in_file, nthreads=1)
results = interface.run(cwd=tmpdir)
assert os.path.isfile(results.outputs.out_file)
denoised_img = nb.load(results.outputs.out_file)
assert denoised_img.shape == in_img.shape
assert os.path.isfile(results.outputs.noise_image)
noise_img = nb.load(results.outputs.noise_image)
assert noise_img.shape == in_img.shape[:3]
assert noise_img.ndim == 3
assert os.path.isfile(results.outputs.out_report)
assert os.path.isfile(results.outputs.nmse_text)
```

**Workflow: Test the get_entity_groups function.** (complexity: 1.00)

```python
'Test the get_entity_groups function.'
bids_dir = tmpdir / 'test_get_entity_groups'
generate_bids_skeleton(str(bids_dir), dset_multipartid)
layout = BIDSLayout(str(bids_dir))
subject_data = {'dwi': layout.get(suffix='dwi', extension='nii.gz', return_type='file')}
entity_groups = grouping.get_entity_groups(layout, subject_data, combine_all_dwis=True)
expected = [['sub-01_acq-98dir_dir-AP_run-2_dwi.nii.gz', 'sub-01_acq-99dir_dir-AP_run-1_dwi.nii.gz'], ['sub-01_acq-99dir_dir-AP_run-3_dwi.nii.gz']]
check_expected(entity_groups, expected)
entity_groups = grouping.get_entity_groups(layout, subject_data, combine_all_dwis=False)
expected = [['sub-01_acq-98dir_dir-AP_run-2_dwi.nii.gz'], ['sub-01_acq-99dir_dir-AP_run-1_dwi.nii.gz'], ['sub-01_acq-99dir_dir-AP_run-3_dwi.nii.gz']]
check_expected(entity_groups, expected)
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 47
**Total Settings:** 919
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 47 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 22
**Categories:** 4

### Overview

- **AGENTS.md** (`AGENTS.md`)
- **README.rst** (`README.rst`)
- **long_description.rst** (`long_description.rst`)

### Contributing

- **CONTRIBUTING.md** (`CONTRIBUTING.md`)

### Other

- **pull_request_template.md** (`.github/pull_request_template.md`)
- **INSTRUCTIONS.md** (`.maint/INSTRUCTIONS.md`)
- **base.rst** (`docs/anat/base.rst`)
- **api.rst** (`docs/api.rst`)
- **changes.md** (`docs/changes.md`)
- *...and 11 more*

### Templates

- **bug_report.md** (`.github/ISSUE_TEMPLATE/bug_report.md`)
- **feature_request.md** (`.github/ISSUE_TEMPLATE/feature_request.md`)

*See `references/documentation/` for all project documentation*

## 📚 Available References

This skill includes detailed reference documentation:

- **Dependencies**: `references/dependencies/` - Dependency graph and analysis
- **Patterns**: `references/patterns/` - Detected design patterns
- **Examples**: `references/test_examples/` - Usage examples from tests
- **Configuration**: `references/config_patterns/` - Configuration patterns
- **Documentation**: `references/documentation/` - Project documentation

---

**Generated by Skill Seeker** | Codebase Analyzer with C3.x Analysis
