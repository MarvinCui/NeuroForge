---
name: nilearn
description: Local codebase analysis for nilearn
doc_version: 
---

# nilearn Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `nilearn`
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

### 🎨 Design Patterns Detected

*From C3.1 codebase analysis (confidence > 0.7)*

- **Adapter**: 1 instances

*Total: 1 high-confidence patterns*

*See `references/patterns/` for complete pattern analysis*

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Workflow: Test nilearn.maskers._mixin._ReportingMixin on concrete masker
instances when ``reports=True``.** (complexity: 1.00)

```python
'Test nilearn.maskers._mixin._ReportingMixin on concrete masker\n    instances when ``reports=True``.\n    '
masker = clone(masker)
assert masker._report_warnings == []
generate_and_check_masker_report(masker, **kwargs)
assert masker._has_report_data() is False
input_img = img_func()
masker.fit(input_img)
assert masker._has_report_data()
extra_warnings_allowed = False
if isinstance(masker, SurfaceMapsMasker):
    extra_warnings_allowed = True
generate_and_check_masker_report(masker, extra_warnings_allowed=extra_warnings_allowed, **kwargs)
generate_and_check_masker_report(masker, title='masker report title', extra_warnings_allowed=extra_warnings_allowed, **kwargs)
masker.reports = False
match = 'Report generation not enabled'
with pytest.warns(UserWarning, match=match):
    report = masker.generate_report(**kwargs)
assert match in str(report)
```

**Workflow: test are array identical** (complexity: 1.00)

```python
arr1 = np.ones(4)
orig1 = arr1.copy()
arr2 = arr1
orig2 = arr2.copy()
assert are_arrays_identical(arr1, arr2)
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
arr2 = arr1[:1]
orig2 = arr2.copy()
assert are_arrays_identical(arr1, arr2)
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
arr2 = arr1[1:]
orig2 = arr2.copy()
assert not are_arrays_identical(arr1, arr2)
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
arr2 = arr1.copy()
orig2 = arr2.copy()
assert not are_arrays_identical(arr1, arr2)
np.testing.assert_array_almost_equal(orig1, arr1, decimal=10)
np.testing.assert_array_almost_equal(orig2, arr2, decimal=10)
```

**Workflow: test as ndarray memmap** (complexity: 1.00)

```python
filename = Path(__file__).parent / 'data' / 'mmap.dat'
arr1 = np.memmap(filename, dtype='float32', mode='w+', shape=(5,))
arr2 = as_ndarray(arr1)
assert not are_arrays_identical(arr1, arr2)
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
arr2 = as_ndarray(arr1, copy=True)
assert not are_arrays_identical(arr1, arr2)
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
arr2 = as_ndarray(arr1, dtype=int)
assert arr2.dtype == int
assert not are_arrays_identical(arr1, arr2)
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(5,))
arr2 = as_ndarray(arr1, dtype=np.float32)
assert arr2.dtype == np.float32
assert not are_arrays_identical(arr1, arr2)
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10))
arr2 = as_ndarray(arr1, order='F')
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
assert arr2.dtype == arr1.dtype
assert not are_arrays_identical(arr1[0], arr2[0])
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10), order='F')
arr2 = as_ndarray(arr1, order='F')
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
assert arr2.dtype == arr1.dtype
assert not are_arrays_identical(arr1[0], arr2[0])
arr1 = np.memmap(filename, dtype='float32', mode='readwrite', shape=(10, 10), order='F')
arr2 = as_ndarray(arr1, order='F', dtype=np.int32)
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
assert arr2.dtype == np.int32
assert not are_arrays_identical(arr1[0], arr2[0])
```

**Workflow: test as ndarray more** (complexity: 1.00)

```python
arr1 = [0, 1, 2, 3]
arr2 = as_ndarray(arr1)
assert not are_arrays_identical(arr1, arr2)
arr1 = [0, 1, 2, 3]
arr2 = as_ndarray(arr1, copy=True)
assert not are_arrays_identical(arr1, arr2)
arr1 = [0, 1, 2, 3]
arr2 = as_ndarray(arr1, dtype=float)
assert arr2.dtype == float
assert not are_arrays_identical(arr1, arr2)
arr1 = [[0, 1, 2, 3], [0, 1, 2, 3]]
arr2 = as_ndarray(arr1, dtype=float, order='F')
assert arr2.dtype == float
assert arr2.flags['F_CONTIGUOUS'] and (not arr2.flags['C_CONTIGUOUS'])
assert not are_arrays_identical(arr1[0], arr2[0])
with pytest.raises(TypeError):
    as_ndarray('test_string')
with pytest.raises(ValueError):
    as_ndarray([], order='invalid')
```

**Workflow: test downloader** (complexity: 1.00)

```python
local_archive = Path(__file__).parent / 'data' / 'craddock_2011_parcellations.tar.gz'
url = 'http://example.com/craddock_atlas'
request_mocker.url_mapping['*craddock*'] = local_archive
datasetdir = tmp_path / 'craddock_2012'
datasetdir.mkdir()
dummy_file = datasetdir / 'random_all.nii.gz'
with dummy_file.open('w') as f:
    f.write('stuff')
opts = {'uncompress': True}
files = [('random_all.nii.gz', url, opts), ('bald.nii.gz', url, opts)]
with pytest.raises(IOError):
    fetch_files(str(tmp_path / 'craddock_2012'), files, verbose=0)
with dummy_file.open('r') as f:
    stuff = f.read(5)
assert stuff == 'stuff'
fetch_atlas_craddock_2012(data_dir=tmp_path)
with dummy_file.open() as f:
    stuff = f.read()
assert stuff == ''
```

**Workflow: test fetch atlas fsl** (complexity: 1.00)

```python
atlas_dir = tmp_path / 'fsl' / 'data' / 'atlases'
nifti_dir = atlas_dir / name
nifti_dir.mkdir(parents=True)
_write_sample_atlas_metadata(atlas_dir, f'{name}{label_fname}', is_symm=is_symm)
target_atlas_nii = nifti_dir / f'{name}-{fname}.nii.gz'
Nifti1Image(atlas_data, affine_eye * 3).to_filename(target_atlas_nii)
atlas_instance = fsl_fetcher(fname, data_dir=tmp_path, symmetric_split=split)
validate_atlas(atlas_instance)
_test_atlas_instance_should_match_data(atlas_instance, is_symm=is_symm or split)
for label in atlas_instance.labels:
    assert label.strip() == label
```

**Workflow: test fetch atlas msdl** (complexity: 1.00)

```python
labels = pd.DataFrame({'x': [1.5, 1.2], 'y': [1.5, 1.3], 'z': [1.5, 1.4], 'name': ['Aud', 'DMN'], 'net name': ['Aud', 'DMN']})
root = Path('MSDL_rois')
archive = {root / 'msdl_rois_labels.csv': labels.to_csv(index=False), root / 'msdl_rois.nii': '', root / 'README.txt': ''}
request_mocker.url_mapping['*MSDL_rois.zip'] = dict_to_archive(archive, 'zip')
dataset = fetch_atlas_msdl(data_dir=tmp_path, verbose=0)
validate_atlas(dataset)
assert isinstance(dataset.region_coords, list)
assert isinstance(dataset.networks, list)
assert isinstance(dataset.maps, str)
assert request_mocker.url_count == 1
check_fetcher_verbosity(fetch_atlas_msdl, capsys, data_dir=tmp_path)
```

**Workflow: test fetch atlas aal** (complexity: 1.00)

```python
metadata = '1\t2\t3\n'
if version == 'SPM12':
    metadata = b"<?xml version='1.0' encoding='us-ascii'?><metadata><label><index>1</index><name>A</name></label></metadata>"
label_file = 'AAL.xml' if version == 'SPM12' else 'ROI_MNI_V4.txt'
atlas_file = 'AAL.nii' if version == 'SPM12' else 'ROI_MNI_V4.nii'
mock_file = tmp_path / f'aal_{version}' / aal_archive_root / atlas_file
mock_file.parent.mkdir(exist_ok=True, parents=True)
img_3d_rand_eye.to_filename(mock_file)
aal_data = dict_to_archive({aal_archive_root / label_file: metadata, aal_archive_root / atlas_file: mock_file}, archive_format=archive_format)
request_mocker.url_mapping[f'*{url_key}*'] = aal_data
dataset = fetch_atlas_aal(version=version, data_dir=tmp_path, verbose=0)
validate_atlas(dataset)
assert isinstance(dataset.maps, str)
assert isinstance(dataset.indices, list)
assert request_mocker.url_count == 1
```

**Workflow: test fetch atlas basc multiscale 2015** (complexity: 1.00)

```python
resolution = 7
dataset_name = 'basc_multiscale_2015'
name_sym = 'template_cambridge_basc_multiscale_nii_sym'
basename_sym = 'template_cambridge_basc_multiscale_sym_scale007.nii.gz'
mock_map = data_gen.generate_labeled_regions((53, 64, 52), resolution)
mock_file = tmp_path / dataset_name / name_sym / basename_sym
mock_file.parent.mkdir(exist_ok=True, parents=True)
mock_map.to_filename(mock_file)
data_sym = fetch_atlas_basc_multiscale_2015(data_dir=tmp_path, verbose=0, resolution=resolution)
validate_atlas(data_sym)
assert data_sym['maps'] == str(tmp_path / dataset_name / name_sym / basename_sym)
name_asym = 'template_cambridge_basc_multiscale_nii_asym'
basename_asym = 'template_cambridge_basc_multiscale_asym_scale007.nii.gz'
mock_file = tmp_path / dataset_name / name_asym / basename_asym
mock_file.parent.mkdir(exist_ok=True, parents=True)
mock_map.to_filename(mock_file)
data_asym = fetch_atlas_basc_multiscale_2015(version='asym', verbose=0, data_dir=tmp_path, resolution=resolution)
validate_atlas(data_asym)
assert data_asym['maps'] == str(tmp_path / dataset_name / name_asym / basename_asym)
check_fetcher_verbosity(fetch_atlas_basc_multiscale_2015, capsys, data_dir=tmp_path)
```

**Workflow: test fetch atlas talairach** (complexity: 1.00)

```python
request_mocker.url_mapping['*talairach.nii'] = _get_small_fake_talairach()
level_values = np.ones((81, 3)) * [0, 1, 2]
talairach = fetch_atlas_talairach('hemisphere', data_dir=tmp_path)
validate_atlas(talairach)
assert_array_equal(get_data(talairach.maps).ravel(), level_values.T.ravel())
assert_array_equal(talairach.labels, ['Background', 'b', 'a'])
talairach = fetch_atlas_talairach('ba', data_dir=tmp_path)
assert_array_equal(get_data(talairach.maps).ravel(), level_values.ravel())
with pytest.raises(ValueError):
    fetch_atlas_talairach('bad_level')
check_fetcher_verbosity(fetch_atlas_talairach, capsys, level_name='hemisphere', data_dir=tmp_path)
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 37
**Total Settings:** 3544
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 37 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 173
**Categories:** 6

### Overview

- **AGENTS.md** (`AGENTS.md`)
- **CLAUDE.md** (`CLAUDE.md`)
- **README.rst** (`README.rst`)

### Examples

- **README.rst** (`examples/00_tutorials/README.rst`)
- **README.rst** (`examples/01_plotting/README.rst`)
- **README.rst** (`examples/02_decoding/README.rst`)
- **README.rst** (`examples/03_connectivity/README.rst`)
- **README.rst** (`examples/04_glm_first_level/README.rst`)
- *...and 5 more*

### Authors

- **AUTHORS.rst** (`AUTHORS.rst`)

### Contributing

- **CONTRIBUTING.rst** (`CONTRIBUTING.rst`)

### Other

- **pull_request_template.md** (`.github/pull_request_template.md`)
- **workflow_failure.md** (`.github/workflow_failure.md`)
- **authors.rst** (`doc/authors.rst`)
- **bibliography.rst** (`doc/bibliography.rst`)
- **gpu_usage.rst** (`doc/building_blocks/gpu_usage.rst`)
- *...and 151 more*

### Templates

- **class.rst** (`doc/templates/class.rst`)
- **function.rst** (`doc/templates/function.rst`)

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
