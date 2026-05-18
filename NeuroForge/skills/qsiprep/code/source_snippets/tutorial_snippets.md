# qsiprep Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Group Dwi Scans With Complex B0Fields

- Kind: `tutorial`
- Source: `references/tutorials/group-dwi-scans-with-complex-b0fields/group-dwi-scans-with-complex-b0fields.md`
- Note: Workflow: Test the group_dwi_scans function. In the test dataset, we have the following:: fmap/ sub-01_dir-AP_epi.nii.gz sub-01_dir-PA_epi.nii.gz dwi/ sub-01_dir-AP_run-1_dwi.nii.gz sub-01_dir-AP_run-2_dwi.nii.gz sub-01_

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test the group_dwi_scans function.\n\n    In the test dataset, we have the following::\n\n    fmap/\n        sub-01_dir-AP_epi.nii.gz\n        sub-01_dir-PA_epi.nii.gz\n    dwi/\n        sub-01_dir-AP_run-1_dwi.nii.gz\n        sub-01_dir-AP_run-2_dwi.nii.gz\n        sub-01_dir-PA_dwi.nii.gz\n\n    The first two DWI runs have different B0 field identifiers, but link to the same fieldmap.\n    The third DWI run has a different B0 field identifier, and links to a different fieldmap.\n\n    We expect the first two DWI runs to be grouped together, and the third DWI run to be grouped\n    separately, based on having the same phase encoding direction.\n    '
bids_dir = tmpdir / 'test_group_dwi_scans_with_complex_b0fields'
dset_yaml = os.path.join(get_test_data_path(), 'skeleton_complex_b0fields.yml')
generate_bids_skeleton(str(bids_dir), dset_yaml)
layout = BIDSLayout(str(bids_dir))
subject_data = {'dwi': layout.get(suffix='dwi', extension='nii.gz', return_type='file')}
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
expected = [{'concatenated_bids_name': 'sub-01_dir-AP', 'dwi_series': ['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], 'dwi_series_pedir': 'j', 'fieldmap_info': {'suffix': None}}, {'concatenated_bids_name': 'sub-01_dir-PA', 'dwi_series': ['sub-01_dir-PA_dwi.nii.gz'], 'dwi_series_pedir': 'j-', 'fieldmap_info': {'suffix': None}}]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=False, ignore_fieldmaps=False)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=False, ignore_fieldmaps=False)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=True)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz', 'sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
```

## 2. How To: Dscsdsi

- Kind: `tutorial`
- Source: `references/tutorials/dscsdsi/dscsdsi.md`
- Note: Workflow: DSCSDSI test Was in DSCSDSI.sh. This tests the following features: - Whether the --anat-only workflow is successful - Whether the regular qsiprep workflow can resume using the working directory from --anat-only

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

## 3. How To: Collect Data

- Kind: `tutorial`
- Source: `references/tutorials/collect-data/collect-data.md`
- Note: Workflow: Test qsiprep.utils.bids.collect_data.

```python
# Setup
# Fixtures: tmpdir, name, skeleton, sessions, n_anats

# Workflow
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

## 4. How To: Dsdti Nofmap

- Kind: `tutorial`
- Source: `references/tutorials/dsdti-nofmap/dsdti-nofmap.md`
- Note: Workflow: DSCDTI_nofmap test. Was in DSDTI_nofmap.sh. This tests the following features: - A workflow with no distortion correction followed by eddy - Eddy is run on a CPU - Denoising is skipped Inputs ------ - DSDTI BID

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

## 5. How To: Dsdti Synfmap

- Kind: `tutorial`
- Source: `references/tutorials/dsdti-synfmap/dsdti-synfmap.md`
- Note: Workflow: DSCDTI_synfmap test Was in DSDTI_synfmap.sh. This tests the following features: - A workflow with no distortion correction followed by eddy - Eddy is run on a CPU - Denoising is skipped Inputs ------ - DSDTI BI

```python
# Setup
# Fixtures: data_dir, output_dir, working_dir

# Workflow
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

## 6. How To: Dscsdsi Fmap

- Kind: `tutorial`
- Source: `references/tutorials/dscsdsi-fmap/dscsdsi-fmap.md`
- Note: Workflow: Run AllFieldmaps test on DSCSDSI data. Was in AllFieldmapsTests.sh. I split it between this and the DSDTI test. XXX: Not called in CircleCI. Instead of running full workflows, this test checks that workflows ca

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

## 7. How To: Dsdti Fmap

- Kind: `tutorial`
- Source: `references/tutorials/dsdti-fmap/dsdti-fmap.md`
- Note: Workflow: Run AllFieldmaps test on DSDTI data. Was in AllFieldmapsTests.sh. I split it between this and the DSCSDSI test. XXX: Not called in CircleCI. Instead of running full workflows, this test checks that workflows ca

```python
# Setup
# Fixtures: data_dir, output_dir, working_dir

# Workflow
'Run AllFieldmaps test on DSDTI data.\n\n    Was in AllFieldmapsTests.sh. I split it between this and the DSCSDSI test.\n    XXX: Not called in CircleCI.\n\n    Instead of running full workflows, this test checks that workflows can\n    be built for all sorts of fieldmap configurations.\n\n    This tests the following features:\n    - Blip-up + Blip-down DWI series for TOPUP/Eddy\n    - Eddy is run on a CPU\n    - dwidenoise is enabled implicitly.\n\n    Inputs\n    ------\n    - DSDTI BIDS data (data/DSDTI_fmap)\n    '
TEST_NAME = 'dsdti_fmap'
dataset_dir = download_test_data('DSDTI_fmap', data_dir)
out_dir = os.path.join(output_dir, TEST_NAME)
work_dir = os.path.join(working_dir, TEST_NAME)
parameters = [dataset_dir, out_dir, 'participant', f'-w={work_dir}', '--boilerplate', '--sloppy', '--write-graph', '--mem-mb=4096', '--output-resolution=5']
_run_and_generate(TEST_NAME, parameters, test_main=False)
```

## 8. How To: Cuda

- Kind: `tutorial`
- Source: `references/tutorials/cuda/cuda.md`
- Note: Workflow: Was in CUDATest.sh. XXX: Not called in CircleCI. This tests the following features: - Blip-up + Blip-down DWI series for TOPUP/Eddy - Eddy is run on a CPU - Denoising is skipped Inputs ------ - DSDTI BIDS data 

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

## 9. How To: Intramodal Template

- Kind: `tutorial`
- Source: `references/tutorials/intramodal-template/intramodal-template.md`
- Note: Workflow: IntramodalTemplate test A two-session dataset is used to create an intramodal template. This tests the following features: - Blip-up + Blip-down DWI series for TOPUP/Eddy - Eddy is run on a CPU - dwidenoise is 

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

## 10. How To: Patch2Self

- Kind: `tutorial`
- Source: `references/tutorials/patch2self/patch2self.md`
- Note: Workflow: Test qsiprep.interfaces.dipy.Patch2Self.

```python
# Setup
# Fixtures: datasets, tmp_path_factory

# Workflow
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

## 11. How To: Get Fieldmaps Relpaths

- Kind: `tutorial`
- Source: `references/tutorials/get-fieldmaps-relpaths/get-fieldmaps-relpaths.md`
- Note: Workflow: Test the get_fieldmaps function.

```python
# Setup
# Fixtures: tmp_path_factory

# Workflow
'Test the get_fieldmaps function.'
base_dir = tmp_path_factory.mktemp('test_get_fieldmaps_relpaths')
bids_dir = base_dir / 'dset_fmap_intendedfor_relpath'
generate_bids_skeleton(str(bids_dir), dset_fmap_intendedfor_relpath)
layout = BIDSLayout(str(bids_dir))
dwi_file = layout.get(suffix='dwi', extension='nii.gz', return_type='file')[0]
fieldmaps = layout.get_fieldmap(dwi_file, return_list=True)
assert len(fieldmaps) == 1
assert fieldmaps[0]['suffix'] == 'epi'
assert layout.get_file(fieldmaps[0]['epi']).get_metadata()['IntendedFor'] == ['dwi/sub-01_dir-AP_dwi.nii.gz']
```

## 12. How To: Drbuddi Shoreline Epi

- Kind: `tutorial`
- Source: `references/tutorials/drbuddi-shoreline-epi/drbuddi-shoreline-epi.md`
- Note: Workflow: Test EPI fieldmap correction with SHORELine + DRBUDDI. Was in DRBUDDI_SHORELine_epi.sh. This tests the following features: - SHORELine (here, just b=0 registration) motion correction

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
