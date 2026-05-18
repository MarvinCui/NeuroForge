# How To: Render Mne Qt Browser

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test adding a mne_qt_browser (and matplotlib) raw plot.

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
# Fixtures: tmp_path, browser_backend
```

## Step-by-Step Guide

### Step 1: 'Test adding a mne_qt_browser (and matplotlib) raw plot.'

```python
'Test adding a mne_qt_browser (and matplotlib) raw plot.'
```

**Verification:**
```python
assert 'MNEBrowseFigure' in name
```

### Step 2: Assign report = Report(...)

```python
report = Report()
```

**Verification:**
```python
assert 'MNEQtBrowser' in name or 'PyQtGraphBrowser' in name
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(1, 1000.0, 'eeg')
```

### Step 4: Assign data = np.zeros(...)

```python
data = np.zeros((1, 1000))
```

### Step 5: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

### Step 6: Assign fig = raw.plot(...)

```python
fig = raw.plot()
```

### Step 7: Assign name = value

```python
name = fig.__class__.__name__
```

### Step 8: Call report.add_figure()

```python
report.add_figure(fig, title='raw')
```

**Verification:**
```python
assert 'MNEBrowseFigure' in name
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, browser_backend

# Workflow
'Test adding a mne_qt_browser (and matplotlib) raw plot.'
report = Report()
info = create_info(1, 1000.0, 'eeg')
data = np.zeros((1, 1000))
raw = RawArray(data, info)
fig = raw.plot()
name = fig.__class__.__name__
if browser_backend.name == 'matplotlib':
    assert 'MNEBrowseFigure' in name
else:
    assert 'MNEQtBrowser' in name or 'PyQtGraphBrowser' in name
report.add_figure(fig, title='raw')
```

## Next Steps


---

*Source: test_report.py:218 | Complexity: Advanced | Last updated: 2026-05-18*