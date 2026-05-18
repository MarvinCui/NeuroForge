# How To: Render Mri

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test rendering MRI for mne report.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `base64`
- `glob`
- `os`
- `pickle`
- `re`
- `shutil`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `matplotlib`
- `mne`
- `mne._fiff.write`
- `mne.datasets`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.report`
- `mne.report`
- `mne.report.report`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `sklearn.exceptions`
- `PIL`
- `pyvista.plotting.plotter`
- `pyvista.plotting.plotting`

**Setup Required:**
```python
# Fixtures: renderer, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test rendering MRI for mne report.'

```python
'Test rendering MRI for mne report.'
```

**Verification:**
```python
assert 'data-mne-tags=" bem "' in html
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert repr(report)
```

### Step 3: Assign trans_fname_new = value

```python
trans_fname_new = tmp_path / 'temp-trans.fif'
```

**Verification:**
```python
assert 'data-mne-tags=" bem "' in html
```

### Step 4: Assign report = Report(...)

```python
report = Report(info_fname=raw_fname, subject='sample', subjects_dir=subjects_dir)
```

**Verification:**
```python
assert 'data-mne-tags=" foo "' in html
```

### Step 5: Call report.parse_folder()

```python
report.parse_folder(data_path=tmp_path, mri_decim=30, pattern='*')
```

### Step 6: Assign fname = value

```python
fname = tmp_path / 'report.html'
```

### Step 7: Call report.save()

```python
report.save(fname, open_browser=False)
```

### Step 8: Assign html = Path.read_text(...)

```python
html = Path(fname).read_text(encoding='utf-8')
```

**Verification:**
```python
assert 'data-mne-tags=" bem "' in html
```

### Step 9: Call report.add_bem()

```python
report.add_bem(subject='sample', title='extra', tags=('foo',), subjects_dir=subjects_dir, decim=30)
```

### Step 10: Call report.save()

```python
report.save(fname, open_browser=False, overwrite=True)
```

### Step 11: Assign html = Path.read_text(...)

```python
html = Path(fname).read_text(encoding='utf-8')
```

**Verification:**
```python
assert 'data-mne-tags=" bem "' in html
```

### Step 12: Call shutil.copyfile()

```python
shutil.copyfile(a, b)
```


## Complete Example

```python
# Setup
# Fixtures: renderer, tmp_path

# Workflow
'Test rendering MRI for mne report.'
pytest.importorskip('nibabel')
trans_fname_new = tmp_path / 'temp-trans.fif'
for a, b in [[trans_fname, trans_fname_new]]:
    shutil.copyfile(a, b)
report = Report(info_fname=raw_fname, subject='sample', subjects_dir=subjects_dir)
report.parse_folder(data_path=tmp_path, mri_decim=30, pattern='*')
fname = tmp_path / 'report.html'
report.save(fname, open_browser=False)
html = Path(fname).read_text(encoding='utf-8')
assert 'data-mne-tags=" bem "' in html
assert repr(report)
report.add_bem(subject='sample', title='extra', tags=('foo',), subjects_dir=subjects_dir, decim=30)
report.save(fname, open_browser=False, overwrite=True)
html = Path(fname).read_text(encoding='utf-8')
assert 'data-mne-tags=" bem "' in html
assert 'data-mne-tags=" foo "' in html
```

## Next Steps


---

*Source: test_report.py:447 | Complexity: Advanced | Last updated: 2026-05-18*