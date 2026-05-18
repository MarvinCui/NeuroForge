# fmriprep Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Bidsuri

- Kind: `tutorial`
- Source: `references/tutorials/bidsuri/bidsuri.md`
- Note: Workflow: Test the BIDSURI interface.

```python
# Workflow
'Test the BIDSURI interface.'
from fmriprep.interfaces.bids import BIDSURI
dataset_links = {'raw': '/data', 'deriv-0': '/data/derivatives/source-1'}
out_dir = '/data/derivatives/fmriprep'
interface = BIDSURI(numinputs=1, dataset_links=dataset_links, out_dir=out_dir)
interface.inputs.in1 = '/data/sub-01/func/sub-01_task-rest_bold.nii.gz'
results = interface.run()
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz']
interface = BIDSURI(numinputs=1, dataset_links=dataset_links, out_dir=out_dir)
interface.inputs.in1 = ['/data/sub-01/func/sub-01_task-rest_bold.nii.gz']
results = interface.run()
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz']
interface = BIDSURI(numinputs=2, dataset_links=dataset_links, out_dir=out_dir)
interface.inputs.in1 = '/data/sub-01/func/sub-01_task-rest_bold.nii.gz'
interface.inputs.in2 = ['/data/derivatives/source-1/sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
results = interface.run()
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:deriv-0:sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
interface = BIDSURI(numinputs=2, dataset_links=dataset_links, out_dir=out_dir)
interface.inputs.in1 = ['/data/sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:raw:sub-01/func/sub-01_task-rest_boldref.nii.gz']
interface.inputs.in2 = ['/data/derivatives/source-1/sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
results = interface.run()
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:raw:sub-01/func/sub-01_task-rest_boldref.nii.gz', 'bids:deriv-0:sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
```

## 2. How To: Convertaffine

- Kind: `tutorial`
- Source: `references/tutorials/convertaffine/convertaffine.md`
- Note: Workflow: test ConvertAffine

```python
# Setup
# Fixtures: tmp_path, data_dir

# Workflow
bold = data_dir / 'sub-pixar008_task-pixar_desc-coreg_boldref.nii.gz'
anat = data_dir / 'sub-pixar008_desc-preproc_T1w.nii.gz'
lta_convert_fsl = nt.linear.load(data_dir / 'mri_coreg-lta_convert.mat', moving=bold, reference=anat, fmt='fsl')
lta_convert_itk = nt.linear.load(data_dir / 'mri_coreg-lta_convert.txt')
c3d_itk = nt.linear.load(data_dir / 'mri_coreg-c3d.txt')
lta_convert_itk_inv = nt.linear.load(data_dir / 'mri_coreg-lta_convert-invert.txt')
c3d_itk_inv = nt.linear.load(data_dir / 'mri_coreg-c3d-invert.txt')
with InGivenDirectory(tmp_path):
    lta_to_fsl = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg.lta', reference=anat, moving=bold, out_fmt='fsl').run()
    assert lta_to_fsl.outputs.out_xfm == str(tmp_path / 'mri_coreg_fwd.mat')
    assert not lta_to_fsl.outputs.out_inv
    nitransforms_fsl = nt.linear.load(lta_to_fsl.outputs.out_xfm, moving=bold, reference=anat, fmt='fsl')
    assert np.allclose(nitransforms_fsl.matrix, lta_convert_fsl.matrix, atol=0.0001)
    lta_to_itk = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg.lta', inverse=True).run()
    assert lta_to_itk.outputs.out_xfm == str(tmp_path / 'mri_coreg_fwd.txt')
    assert lta_to_itk.outputs.out_inv == str(tmp_path / 'mri_coreg_inv.txt')
    nitransforms_itk = nt.linear.load(lta_to_itk.outputs.out_xfm)
    assert np.allclose(nitransforms_itk.matrix, lta_convert_itk.matrix, atol=0.0001)
    assert np.allclose(nitransforms_itk.matrix, c3d_itk.matrix, atol=0.0001)
    nitransforms_itk_inv = nt.linear.load(lta_to_itk.outputs.out_inv)
    assert np.allclose(nitransforms_itk_inv.matrix, lta_convert_itk_inv.matrix, atol=0.0001)
    assert np.allclose(nitransforms_itk_inv.matrix, c3d_itk_inv.matrix, atol=0.0001)
    fsl_to_itk = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg-lta_convert.mat', reference=anat, moving=bold, out_fmt='itk', inverse=True).run()
    nitransforms_itk = nt.linear.load(fsl_to_itk.outputs.out_xfm)
    assert np.allclose(nitransforms_itk.matrix, lta_convert_itk.matrix, atol=0.0001)
    assert np.allclose(nitransforms_itk.matrix, c3d_itk.matrix, atol=0.0001)
    nitransforms_itk_inv = nt.linear.load(fsl_to_itk.outputs.out_inv)
    assert np.allclose(nitransforms_itk_inv.matrix, lta_convert_itk_inv.matrix, atol=0.0001)
    assert np.allclose(nitransforms_itk_inv.matrix, c3d_itk_inv.matrix, atol=0.0001)
```

## 3. How To: Reuse Config

- Kind: `tutorial`
- Source: `references/tutorials/reuse-config/reuse-config.md`
- Note: Workflow: test reuse config

```python
# Setup
# Fixtures: tmp_path

# Workflow
from niworkflows.utils.testing import generate_bids_skeleton
bids_dir = tmp_path / 'ds000005'
generate_bids_skeleton(bids_dir, {'01': {'anat': {'suffix': 'T1w'}}})
cli_args = [str(bids_dir), str(tmp_path / 'out'), 'participant', '--skip-bids-validation']
parse_args(cli_args)
default_config = config.get(flat=True)
assert default_config['execution.output_spaces'] == 'MNI152NLin2009cAsym:res-native'
_reset_config()
config_file = data.load('tests/config.toml')
config_args = ['--config-file', str(config_file)]
parse_args(cli_args + config_args)
reused_config = config.get(flat=True)
assert reused_config['execution.output_spaces'] == 'MNI152NLin2009cAsym:res-2 MNI152NLin2009cAsym:res-native fsaverage:den-10k fsaverage:den-30k'
assert reused_config['execution.log_dir'] not in config_file.read_text()
_reset_config()
overridden_args = cli_args + config_args + ['--output-spaces', 'MNI152NLin6Asym', '--force', 'bbr']
overridden_args[1] = str(tmp_path / 'out2')
parse_args(overridden_args)
overridden_config = config.get(flat=True)
assert overridden_config['execution.output_spaces'] == 'MNI152NLin6Asym:res-native'
assert 'bbr' in overridden_config['workflow.force']
for v in ('execution.run_uuid', 'execution.fmriprep_dir'):
    assert reused_config[v] != overridden_config[v]
_reset_config()
```

## 4. How To: Derivatives

- Kind: `tutorial`
- Source: `references/tutorials/derivatives/derivatives.md`
- Note: Workflow: Check the correct parsing of the derivatives argument.

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check the correct parsing of the derivatives argument.'
bids_path = tmp_path / 'data'
out_path = tmp_path / 'out'
args = [str(bids_path), str(out_path), 'participant']
bids_path.mkdir()
parser = _build_parser()
temp_args = args + ['--derivatives']
with pytest.raises((SystemExit, ArgumentError)):
    parser.parse_args(temp_args)
_reset_config()
temp_args = args + ['--derivatives', str(bids_path / 'derivatives/smriprep')]
opts = parser.parse_args(temp_args)
assert opts.derivatives == {'smriprep': bids_path / 'derivatives/smriprep'}
_reset_config()
temp_args = args + ['--derivatives', f"anat={bids_path / 'derivatives/smriprep'}"]
opts = parser.parse_args(temp_args)
assert opts.derivatives == {'anat': bids_path / 'derivatives/smriprep'}
_reset_config()
temp_args = args + ['--derivatives', str(bids_path / 'derivatives_01/smriprep'), str(bids_path / 'derivatives_02/smriprep')]
with pytest.raises(ValueError, match='Received duplicate derivative name'):
    parser.parse_args(temp_args)
_reset_config()
```

## 5. How To: Config Spaces

- Kind: `tutorial`
- Source: `references/tutorials/config-spaces/config-spaces.md`
- Note: Workflow: Check that all necessary spaces are recorded in the config.

```python
# Workflow
'Check that all necessary spaces are recorded in the config.'
settings = loads(data.load.readable('tests/config.toml').read_text())
for sectionname, configs in settings.items():
    if sectionname != 'environment':
        section = getattr(config, sectionname)
        section.load(configs, init=False)
config.nipype.init()
config.loggers.init()
config.init_spaces()
spaces = config.workflow.spaces
assert 'MNI152NLin6Asym:res-1' not in [str(s) for s in spaces.get_standard(full_spec=True)]
assert 'MNI152NLin6Asym_res-1' not in [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3]
config.workflow.cifti_output = True
config.init_spaces()
spaces = config.workflow.spaces
assert 'MNI152NLin6Asym:res-1' in [str(s) for s in spaces.get_standard(full_spec=True)]
assert 'MNI152NLin6Asym_res-1' in [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3]
config.execution.output_spaces = None
config.workflow.cifti_output = False
config.init_spaces()
spaces = config.workflow.spaces
assert [str(s) for s in spaces.get_standard(full_spec=True)] == []
assert [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3] == ['MNI152NLin2009cAsym']
_reset_config()
```

## 6. How To: Bidssourcefile

- Kind: `tutorial`
- Source: `references/tutorials/bidssourcefile/bidssourcefile.md`
- Note: Workflow: Test the BIDSSourceFile interface

```python
# Setup
# Fixtures: bids_info_anat, bids_info_func, precomputed_infos

# Workflow
'Test the BIDSSourceFile interface'
from fmriprep.interfaces.bids import BIDSSourceFile
interface = BIDSSourceFile()
anat_type = next(iter(bids_info_anat))
interface.inputs.anat_type = anat_type
interface.inputs.bids_info = {**bids_info_anat, **bids_info_func}
interface.inputs.precomputed = precomputed_infos
results = interface.run()
if precomputed_infos:
    bold = 'sub-01/func/sub-01_bold.nii.gz' if isinstance(bids_info_func['bold'][0], list) else 'sub-01/func/sub-01_task-rest_bold.nii.gz'
    assert results.outputs.source_file == bold
else:
    assert results.outputs.source_file == bids_info_anat[anat_type][0]
```

## 7. How To: Bold Wf

- Kind: `tutorial`
- Source: `references/tutorials/bold-wf/bold-wf.md`
- Note: Workflow: Test as many combinations of precomputed files and input configurations as possible.

```python
# Setup
# Fixtures: bids_root, tmp_path, task, fieldmap_id, freesurfer, level, bold2anat_init

# Workflow
'Test as many combinations of precomputed files and input\n    configurations as possible.'
output_dir = tmp_path / 'output'
output_dir.mkdir()
img = nb.Nifti1Image(np.zeros((10, 10, 10, 10)), np.eye(4))
if task == 'rest':
    bold_series = [str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_bold.nii.gz')]
    sbref = str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_sbref.nii.gz')
elif task == 'nback':
    bold_series = [str(bids_root / 'sub-01' / 'func' / f'sub-01_task-nback_echo-{i}_bold.nii.gz') for i in range(1, 4)]
    sbref = str(bids_root / 'sub-01' / 'func' / 'sub-01_task-nback_echo-1_sbref.nii.gz')
for path in bold_series:
    img.to_filename(path)
img.to_filename(sbref)
with mock_config(bids_dir=bids_root):
    config.workflow.bold2anat_init = bold2anat_init
    config.workflow.level = level
    config.workflow.run_reconall = freesurfer
    wf = init_bold_wf(bold_series=bold_series, fieldmap_id=fieldmap_id, precomputed={})
flatgraph = wf._create_flat_graph()
generate_expanded_graph(flatgraph)
```

## 8. How To: Clip

- Kind: `tutorial`
- Source: `references/tutorials/clip/clip.md`
- Note: Workflow: test Clip

```python
# Setup
# Fixtures: tmp_path

# Workflow
in_file = str(tmp_path / 'input.nii')
data = np.array([[[-1.0, 1.0], [-2.0, 2.0]]])
nb.Nifti1Image(data, np.eye(4)).to_filename(in_file)
threshold = pe.Node(Clip(in_file=in_file, minimum=0), name='threshold', base_dir=tmp_path)
ret = threshold.run()
assert ret.outputs.out_file == str(tmp_path / 'threshold/input_clipped.nii')
out_img = nb.load(ret.outputs.out_file)
assert np.allclose(out_img.get_fdata(), [[[0.0, 1.0], [0.0, 2.0]]])
threshold2 = pe.Node(Clip(in_file=in_file, minimum=-3), name='threshold2', base_dir=tmp_path)
ret = threshold2.run()
assert ret.outputs.out_file == in_file
out_img = nb.load(ret.outputs.out_file)
assert np.allclose(out_img.get_fdata(), [[[-1.0, 1.0], [-2.0, 2.0]]])
clip = pe.Node(Clip(in_file=in_file, minimum=-1, maximum=1), name='clip', base_dir=tmp_path)
ret = clip.run()
assert ret.outputs.out_file == str(tmp_path / 'clip/input_clipped.nii')
out_img = nb.load(ret.outputs.out_file)
assert np.allclose(out_img.get_fdata(), [[[-1.0, 1.0], [-1.0, 1.0]]])
nonpositive = pe.Node(Clip(in_file=in_file, maximum=0), name='nonpositive', base_dir=tmp_path)
ret = nonpositive.run()
assert ret.outputs.out_file == str(tmp_path / 'nonpositive/input_clipped.nii')
out_img = nb.load(ret.outputs.out_file)
assert np.allclose(out_img.get_fdata(), [[[-1.0, 0.0], [-2.0, 0.0]]])
```

## 9. How To: Fmriprep Wf Heterogeneous Sessions

- Kind: `tutorial`
- Source: `references/tutorials/fmriprep-wf-heterogeneous-sessions/fmriprep-wf-heterogeneous-sessions.md`
- Note: Workflow: Test on a heterogeneous sessions layout, and test track_sessions behavior

```python
# Setup
# Fixtures: bids_root_factory

# Workflow
'Test on a heterogeneous sessions layout, and test track_sessions behavior'
bids_dir = bids_root_factory('heterogeneous_sessions')
with mock_config(bids_dir=bids_dir):
    config.workflow.bold2anat_init = 't1w'
    config.workflow.track_sessions = True
    procs = config._create_processing_groups()
    assert procs == [('01', ['anat', 'fmri'])]
    wf = init_fmriprep_wf()
    assert wf.get_node('sub_01_ses_anat-fmri_wf')
    config.workflow.track_sessions = False
    procs = config._create_processing_groups()
    assert procs == [('01', None)]
    wf = init_fmriprep_wf()
    assert wf.get_node('sub_01_wf')
```

## 10. How To: Bold Native Precomputes

- Kind: `tutorial`
- Source: `references/tutorials/bold-native-precomputes/bold-native-precomputes.md`
- Note: Workflow: Test as many combinations of precomputed files and input configurations as possible.

```python
# Setup
# Fixtures: bids_root, tmp_path, task, fieldmap_id, run_stc

# Workflow
'Test as many combinations of precomputed files and input\n    configurations as possible.'
output_dir = tmp_path / 'output'
output_dir.mkdir()
img = nb.Nifti1Image(np.zeros((10, 10, 10, 10)), np.eye(4))
if task == 'rest':
    bold_series = [str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_bold.nii.gz')]
elif task == 'nback':
    bold_series = [str(bids_root / 'sub-01' / 'func' / f'sub-01_task-nback_echo-{i}_bold.nii.gz') for i in range(1, 4)]
for path in bold_series:
    img.to_filename(path)
with mock_config(bids_dir=bids_root):
    config.workflow.ignore = ['slicetiming'] if not run_stc else []
    wf = init_bold_native_wf(bold_series=bold_series, fieldmap_id=fieldmap_id, omp_nthreads=1)
flatgraph = wf._create_flat_graph()
generate_expanded_graph(flatgraph)
```

## 11. How To: Get Estimator Multiple B0Fields

- Kind: `tutorial`
- Source: `references/tutorials/get-estimator-multiple-b0fields/get-estimator-multiple-b0fields.md`
- Note: Workflow: test get estimator multiple b0fields

```python
# Setup
# Fixtures: tmp_path

# Workflow
bids_dir = tmp_path / 'bids'
spec = get_layout('no_session')
spec['01']['func'][0]['metadata']['B0FieldSource'] = ('epi', 'phasediff')
spec['01']['func'][1]['metadata']['B0FieldSource'] = 'epi'
spec['01']['fmap'][0]['metadata']['B0FieldIdentifier'] = 'phasediff'
spec['01']['fmap'][1]['metadata']['B0FieldIdentifier'] = 'phasediff'
spec['01']['fmap'][2]['metadata']['B0FieldIdentifier'] = 'epi'
spec['01']['fmap'][3]['metadata']['B0FieldIdentifier'] = 'epi'
generate_bids_skeleton(bids_dir, spec)
layout = bids.BIDSLayout(bids_dir)
_ = find_estimators(layout=layout, subject='01')
bold_files = sorted(layout.get(suffix='bold', task='rest', extension='.nii.gz', return_type='file'))
assert get_estimator(layout, bold_files[0]) == ['epi', 'phasediff']
assert get_estimator(layout, bold_files[1]) == ('epi',)
```

## 12. How To: Bids Filter File

- Kind: `tutorial`
- Source: `references/tutorials/bids-filter-file/bids-filter-file.md`
- Note: Workflow: test bids filter file

```python
# Setup
# Fixtures: tmp_path, capsys

# Workflow
bids_path = tmp_path / 'data'
out_path = tmp_path / 'out'
bff = tmp_path / 'filter.json'
args = [str(bids_path), str(out_path), 'participant', '--bids-filter-file', str(bff)]
bids_path.mkdir()
parser = _build_parser()
with pytest.raises(SystemExit):
    parser.parse_args(args)
err = capsys.readouterr().err
assert 'Path does not exist:' in err
bff.write_text('{"invalid json": }')
with pytest.raises(SystemExit):
    parser.parse_args(args)
err = capsys.readouterr().err
assert 'JSON syntax error in:' in err
_reset_config()
```
