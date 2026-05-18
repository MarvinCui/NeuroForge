---
name: fmriprep
description: Local codebase analysis for fmriprep
doc_version: 
---

# fmriprep Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `fmriprep`
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

**Workflow: test bids filter file** (complexity: 1.00)

```python
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

**Workflow: test use syn sdc** (complexity: 1.00)

```python
bids_path = tmp_path / 'data'
out_path = tmp_path / 'out'
args = [str(bids_path), str(out_path), 'participant'] + args
bids_path.mkdir()
parser = _build_parser()
cm = nullcontext()
if isinstance(expectation, tuple):
    cm = pytest.raises(expectation)
with cm:
    opts = parser.parse_args(args)
if not isinstance(expectation, tuple):
    assert opts.use_syn_sdc == expectation
_reset_config()
```

**Workflow: Check the correct parsing of the derivatives argument.** (complexity: 1.00)

```python
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

**Workflow: test reuse config** (complexity: 1.00)

```python
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

**Workflow: Check that all necessary spaces are recorded in the config.** (complexity: 1.00)

```python
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

**Workflow: test Clip** (complexity: 1.00)

```python
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

**Workflow: Test the BIDSURI interface.** (complexity: 1.00)

```python
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

**Workflow: Test as many combinations of precomputed files and input
configurations as possible.** (complexity: 1.00)

```python
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

**Workflow: test RenameACompCor** (complexity: 1.00)

```python
renamer = pe.Node(confounds.RenameACompCor(), name='renamer', base_dir=str(tmp_path))
renamer.inputs.components_file = data_dir / 'acompcor_truncated.tsv'
renamer.inputs.metadata_file = data_dir / 'component_metadata_truncated.tsv'
res = renamer.run()
target_components = Path.read_text(data_dir / 'acompcor_renamed.tsv')
target_meta = Path.read_text(data_dir / 'component_metadata_renamed.tsv')
renamed_components = Path(res.outputs.components_file).read_text()
renamed_meta = Path(res.outputs.metadata_file).read_text()
assert renamed_components == target_components
assert renamed_meta == target_meta
```

**Workflow: test FSLMotionParams** (complexity: 1.00)

```python
base = 'sub-01_task-mixedgamblestask_run-01'
xfms = data_dir / f'{base}_from-orig_to-boldref_mode-image_desc-hmc_xfm.txt'
boldref = data_dir / f'{base}_desc-hmc_boldref.nii.gz'
orig_timeseries = data_dir / f'{base}_desc-motion_timeseries.tsv'
motion = pe.Node(confounds.FSLMotionParams(xfm_file=str(xfms), boldref_file=str(boldref)), name='fsl_motion', base_dir=str(tmp_path))
res = motion.run()
derived_params = pd.read_csv(res.outputs.out_file, sep='\t')
orig_params = pd.read_csv(orig_timeseries, sep='\t')[derived_params.columns]
limits = pd.DataFrame({'trans_x': [0.0001], 'trans_y': [0.0001], 'trans_z': [0.0001], 'rot_x': [1e-06], 'rot_y': [1e-06], 'rot_z': [1e-06]})
max_diff = (orig_params - derived_params).abs().max()
assert np.all(max_diff < limits)
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 32
**Total Settings:** 655
**Patterns Detected:** 1

**Configuration Types:**
- unknown: 32 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 26
**Categories:** 5

### Overview

- **CHANGES.rst** (`CHANGES.rst`)
- **GOVERNANCE.md** (`GOVERNANCE.md`)
- **README.rst** (`README.rst`)
- **REFERENCES.md** (`REFERENCES.md`)
- **long_description.rst** (`long_description.rst`)

### Community

- **CODE_OF_CONDUCT.md** (`CODE_OF_CONDUCT.md`)

### Contributing

- **CONTRIBUTING.md** (`CONTRIBUTING.md`)

### Other

- **CONTRIBUTORS.md** (`.maint/CONTRIBUTORS.md`)
- **FORMER.md** (`.maint/FORMER.md`)
- **MAINTAINERS.md** (`.maint/MAINTAINERS.md`)
- **PIs.md** (`.maint/PIs.md`)
- **api.rst** (`docs/api.rst`)
- *...and 13 more*

### Templates

- **documentation.md** (`.github/ISSUE_TEMPLATE/documentation.md`)

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
