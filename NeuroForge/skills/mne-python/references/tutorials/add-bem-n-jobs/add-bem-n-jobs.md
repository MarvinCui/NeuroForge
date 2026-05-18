# How To: Add Bem N Jobs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test add_bem with n_jobs.

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
# Fixtures: n_jobs, monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test add_bem with n_jobs.'

```python
'Test add_bem with n_jobs.'
```

**Verification:**
```python
assert len(report.html) == 1
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert imgs.ndim == 4
```

### Step 3: Assign report = Report(...)

```python
report = Report(subjects_dir=use_subjects_dir, image_format='png')
```

**Verification:**
```python
assert len(imgs) == 6
```

### Step 4: Call monkeypatch.setattr()

```python
monkeypatch.setattr(report_mod, '_BEM_VIEWS', ('axial',))
```

**Verification:**
```python
assert 0.778 < corr < 0.8
```

### Step 5: Call report.add_bem()

```python
report.add_bem(subject='sample', title='sample', tags=('sample',), decim=15, n_jobs=n_jobs, subjects_dir=subjects_dir)
```

**Verification:**
```python
assert len(report.html) == 1
```

### Step 6: Assign imgs = np.array(...)

```python
imgs = np.array([plt.imread(BytesIO(base64.b64decode(b)), 'png') for b in re.findall('data:image/png;base64,(\\S*)">', report.html[0])])
```

**Verification:**
```python
assert imgs.ndim == 4
```

### Step 7: Assign imgs = _reshape_view(...)

```python
imgs = _reshape_view(imgs, (len(imgs), -1))
```

### Step 8: Assign norms = np.linalg.norm(...)

```python
norms = np.linalg.norm(imgs, axis=-1)
```

### Step 9: Assign corr = value

```python
corr = np.corrcoef(norms, np.hanning(len(imgs)))[0, 1]
```

**Verification:**
```python
assert 0.778 < corr < 0.8
```

### Step 10: Assign use_subjects_dir = None

```python
use_subjects_dir = None
```

### Step 11: Assign use_subjects_dir = subjects_dir

```python
use_subjects_dir = subjects_dir
```

### Step 12: Assign use_subjects_dir = None

```python
use_subjects_dir = None
```


## Complete Example

```python
# Setup
# Fixtures: n_jobs, monkeypatch

# Workflow
'Test add_bem with n_jobs.'
pytest.importorskip('nibabel')
if n_jobs == 1:
    use_subjects_dir = None
else:
    use_subjects_dir = subjects_dir
report = Report(subjects_dir=use_subjects_dir, image_format='png')
monkeypatch.setattr(report_mod, '_BEM_VIEWS', ('axial',))
if use_subjects_dir is not None:
    use_subjects_dir = None
report.add_bem(subject='sample', title='sample', tags=('sample',), decim=15, n_jobs=n_jobs, subjects_dir=subjects_dir)
assert len(report.html) == 1
imgs = np.array([plt.imread(BytesIO(base64.b64decode(b)), 'png') for b in re.findall('data:image/png;base64,(\\S*)">', report.html[0])])
assert imgs.ndim == 4
assert len(imgs) == 6
imgs = _reshape_view(imgs, (len(imgs), -1))
norms = np.linalg.norm(imgs, axis=-1)
corr = np.corrcoef(norms, np.hanning(len(imgs)))[0, 1]
assert 0.778 < corr < 0.8
```

## Next Steps


---

*Source: test_report.py:482 | Complexity: Advanced | Last updated: 2026-05-18*