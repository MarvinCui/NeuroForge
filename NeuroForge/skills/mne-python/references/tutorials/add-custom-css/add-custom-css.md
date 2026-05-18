# How To: Add Custom Css

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test adding custom CSS rules to the report.

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

### Step 1: 'Test adding custom CSS rules to the report.'

```python
'Test adding custom CSS rules to the report.'
```

**Verification:**
```python
assert custom_css in report.include
```

### Step 2: Assign fname = value

```python
fname = tmp_path / 'report.html'
```

**Verification:**
```python
assert custom_css in html
```

### Step 3: Assign fig = plt.figure(...)

```python
fig = plt.figure()
```

### Step 4: Assign report = Report(...)

```python
report = Report()
```

### Step 5: Call report.add_figure()

```python
report.add_figure(fig=fig, title='Test section')
```

### Step 6: Assign custom_css = '.report_custom { color: red; }'

```python
custom_css = '.report_custom { color: red; }'
```

### Step 7: Call report.add_custom_css()

```python
report.add_custom_css(css=custom_css)
```

**Verification:**
```python
assert custom_css in report.include
```

### Step 8: Call report.save()

```python
report.save(fname, open_browser=False)
```

### Step 9: Assign html = Path.read_text(...)

```python
html = Path(fname).read_text(encoding='utf-8')
```

**Verification:**
```python
assert custom_css in html
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test adding custom CSS rules to the report.'
fname = tmp_path / 'report.html'
fig = plt.figure()
report = Report()
report.add_figure(fig=fig, title='Test section')
custom_css = '.report_custom { color: red; }'
report.add_custom_css(css=custom_css)
assert custom_css in report.include
report.save(fname, open_browser=False)
html = Path(fname).read_text(encoding='utf-8')
assert custom_css in html
```

## Next Steps


---

*Source: test_report.py:264 | Complexity: Advanced | Last updated: 2026-05-18*