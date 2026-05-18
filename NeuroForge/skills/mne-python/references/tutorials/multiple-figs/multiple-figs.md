# How To: Multiple Figs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test adding a slider with a series of figures to a Report.

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

### Step 1: 'Test adding a slider with a series of figures to a Report.'

```python
'Test adding a slider with a series of figures to a Report.'
```

**Verification:**
```python
assert report._content[0].name == 'my title'
```

### Step 2: Assign report = Report(...)

```python
report = Report(info_fname=raw_fname, subject='sample', subjects_dir=subjects_dir)
```

### Step 3: Assign figs = _get_example_figures(...)

```python
figs = _get_example_figures()
```

### Step 4: Call report.add_figure()

```python
report.add_figure(fig=figs, title='my title')
```

**Verification:**
```python
assert report._content[0].name == 'my title'
```

### Step 5: Call report.save()

```python
report.save(tmp_path / 'report.html', open_browser=False)
```

### Step 6: Assign report = Report(...)

```python
report = Report()
```

### Step 7: Assign unknown = plt.subplots(...)

```python
fig, ax = plt.subplots()
```

### Step 8: Call ax.set_xlabel()

```python
ax.set_xlabel('µ')
```

### Step 9: Call report.add_figure()

```python
report.add_figure(fig=[fig] * 2, title='title', image_format='svg')
```

### Step 10: Call report.add_figure()

```python
report.add_figure(fig=figs, title='title', caption=['wug'])
```

### Step 11: Call report.add_figure()

```python
report.add_figure(fig=figs, title='title', caption='wug')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test adding a slider with a series of figures to a Report.'
report = Report(info_fname=raw_fname, subject='sample', subjects_dir=subjects_dir)
figs = _get_example_figures()
report.add_figure(fig=figs, title='my title')
assert report._content[0].name == 'my title'
report.save(tmp_path / 'report.html', open_browser=False)
with pytest.raises(ValueError):
    report.add_figure(fig=figs, title='title', caption=['wug'])
with pytest.raises(ValueError, match='Number of captions.*must be equal to.*figures'):
    report.add_figure(fig=figs, title='title', caption='wug')
report = Report()
fig, ax = plt.subplots()
ax.set_xlabel('µ')
report.add_figure(fig=[fig] * 2, title='title', image_format='svg')
```

## Next Steps


---

*Source: test_report.py:572 | Complexity: Advanced | Last updated: 2026-05-18*