# How To: Render Non Fiff

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test rendering non-FIFF files for mne report.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test rendering non-FIFF files for mne report.'

```python
'Test rendering non-FIFF files for mne report.'
```

**Verification:**
```python
assert Path(fname).name in [Path(x).name for x in content_titles]
```

### Step 2: Assign fnames_in = value

```python
fnames_in = [bdf_fname, edf_fname]
```

**Verification:**
```python
assert len(content_titles) == len(fnames_out)
```

### Step 3: Assign fnames_out = value

```python
fnames_out = []
```

**Verification:**
```python
assert 'test_raw.bdf' in html
```

### Step 4: Assign report = Report(...)

```python
report = Report()
```

**Verification:**
```python
assert 'test_raw.edf' in html
```

### Step 5: Call report.parse_folder()

```python
report.parse_folder(data_path=tmp_path, render_bem=False, on_error='raise', raw_butterfly=False)
```

### Step 6: Assign unknown = report._content_as_html(...)

```python
_, _, content_titles, _ = report._content_as_html()
```

**Verification:**
```python
assert len(content_titles) == len(fnames_out)
```

### Step 7: Assign report.data_path = tmp_path

```python
report.data_path = tmp_path
```

### Step 8: Assign fname = value

```python
fname = tmp_path / 'report.html'
```

### Step 9: Call report.save()

```python
report.save(fname=fname, open_browser=False)
```

### Step 10: Assign html = fname.read_text(...)

```python
html = fname.read_text(encoding='utf-8')
```

**Verification:**
```python
assert 'test_raw.bdf' in html
```

### Step 11: Assign basename = value

```python
basename = fname.stem
```

### Step 12: Assign ext = value

```python
ext = fname.suffix
```

### Step 13: Assign fname_out = value

```python
fname_out = f'{basename}_raw{ext}'
```

### Step 14: Assign outpath = value

```python
outpath = tmp_path / fname_out
```

### Step 15: Call shutil.copyfile()

```python
shutil.copyfile(fname, outpath)
```

### Step 16: Call fnames_out.append()

```python
fnames_out.append(fname_out)
```

**Verification:**
```python
assert Path(fname).name in [Path(x).name for x in content_titles]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test rendering non-FIFF files for mne report.'
fnames_in = [bdf_fname, edf_fname]
fnames_out = []
for fname in fnames_in:
    basename = fname.stem
    ext = fname.suffix
    fname_out = f'{basename}_raw{ext}'
    outpath = tmp_path / fname_out
    shutil.copyfile(fname, outpath)
    fnames_out.append(fname_out)
report = Report()
report.parse_folder(data_path=tmp_path, render_bem=False, on_error='raise', raw_butterfly=False)
_, _, content_titles, _ = report._content_as_html()
for fname in content_titles:
    assert Path(fname).name in [Path(x).name for x in content_titles]
assert len(content_titles) == len(fnames_out)
report.data_path = tmp_path
fname = tmp_path / 'report.html'
report.save(fname=fname, open_browser=False)
html = fname.read_text(encoding='utf-8')
assert 'test_raw.bdf' in html
assert 'test_raw.edf' in html
```

## Next Steps


---

*Source: test_report.py:297 | Complexity: Advanced | Last updated: 2026-05-18*