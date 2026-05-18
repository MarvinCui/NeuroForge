# How To: Render Report Extra

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test SVG and projector rendering separately.

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
# Fixtures: renderer_pyvistaqt, tmp_path, invisible_fig
```

## Step-by-Step Guide

### Step 1: 'Test SVG and projector rendering separately.'

```python
'Test SVG and projector rendering separately.'
```

**Verification:**
```python
assert repr(report)
```

### Step 2: Assign raw_fname_new = value

```python
raw_fname_new = tmp_path / 'temp_raw.fif'
```

**Verification:**
```python
assert fname.is_file()
```

### Step 3: Call shutil.copyfile()

```python
shutil.copyfile(raw_fname, raw_fname_new)
```

**Verification:**
```python
assert 'Projectors' in html
```

### Step 4: Assign report = Report(...)

```python
report = Report(info_fname=raw_fname_new, subjects_dir=subjects_dir, projs=True, image_format='svg')
```

**Verification:**
```python
assert repr(report)
```

### Step 5: Assign report.data_path = tmp_path

```python
report.data_path = tmp_path
```

### Step 6: Assign fname = value

```python
fname = tmp_path / 'report.html'
```

### Step 7: Call report.save()

```python
report.save(fname=fname, open_browser=False)
```

**Verification:**
```python
assert fname.is_file()
```

### Step 8: Assign html = fname.read_text(...)

```python
html = fname.read_text(encoding='utf-8')
```

**Verification:**
```python
assert 'Projectors' in html
```

### Step 9: Call report.parse_folder()

```python
report.parse_folder(data_path=tmp_path, on_error='raise', n_time_points_evokeds=2, raw_butterfly=False, stc_plot_kwargs=stc_plot_kwargs, topomap_kwargs=topomap_kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_pyvistaqt, tmp_path, invisible_fig

# Workflow
'Test SVG and projector rendering separately.'
raw_fname_new = tmp_path / 'temp_raw.fif'
shutil.copyfile(raw_fname, raw_fname_new)
report = Report(info_fname=raw_fname_new, subjects_dir=subjects_dir, projs=True, image_format='svg')
with pytest.warns(RuntimeWarning, match='Cannot render MRI'):
    report.parse_folder(data_path=tmp_path, on_error='raise', n_time_points_evokeds=2, raw_butterfly=False, stc_plot_kwargs=stc_plot_kwargs, topomap_kwargs=topomap_kwargs)
assert repr(report)
report.data_path = tmp_path
fname = tmp_path / 'report.html'
report.save(fname=fname, open_browser=False)
assert fname.is_file()
html = fname.read_text(encoding='utf-8')
assert 'Projectors' in html
```

## Next Steps


---

*Source: test_report.py:234 | Complexity: Advanced | Last updated: 2026-05-18*