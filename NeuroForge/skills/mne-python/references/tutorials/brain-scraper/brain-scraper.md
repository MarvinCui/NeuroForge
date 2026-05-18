# How To: Brain Scraper

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test a simple scraping example.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `platform`
- `contextlib`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `matplotlib`
- `matplotlib.lines`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.utils`
- `mne.viz`
- `mne.viz._brain`
- `mne.viz._brain.colormap`
- `mne.viz.utils`
- `mne.viz._brain`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: renderer_interactive_pyvistaqt, brain_gc, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test a simple scraping example.'

```python
'Test a simple scraping example.'
```

**Verification:**
```python
assert brain.plotter is None
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sphinx_gallery')
```

**Verification:**
```python
assert brain._cleaned
```

### Step 3: Assign stc = read_source_estimate(...)

```python
stc = read_source_estimate(fname_stc, subject='sample')
```

**Verification:**
```python
assert fname.stem in rst
```

### Step 4: Assign size = value

```python
size = (600, 400)
```

**Verification:**
```python
assert fname.is_file()
```

### Step 5: Assign brain = stc.plot(...)

```python
brain = stc.plot(subjects_dir=subjects_dir, time_viewer=True, show_traces=True, hemi='split', size=size, views='lat')
```

**Verification:**
```python
assert np.isclose(w, w0, atol=30) or np.isclose(w, w0 * 2, atol=30), f'w ∉ {{{w0}, {2 * w0}}}'
```

### Step 6: Assign fnames = value

```python
fnames = [str(tmp_path / f'temp_{ii}.png') for ii in range(2)]
```

### Step 7: Assign block_vars = dict(...)

```python
block_vars = dict(image_path_iterator=iter(fnames), example_globals=dict(brain=brain))
```

### Step 8: Assign block = value

```python
block = ('code', '', 1)
```

### Step 9: Assign gallery_conf = dict(...)

```python
gallery_conf = dict(src_dir=str(tmp_path), compress_images=[], image_srcset=[], matplotlib_animations=(False, None))
```

### Step 10: Assign scraper = _BrainScraper(...)

```python
scraper = _BrainScraper()
```

### Step 11: Assign rst = scraper(...)

```python
rst = scraper(block, block_vars, gallery_conf)
```

**Verification:**
```python
assert brain.plotter is None
```

### Step 12: Assign fname = Path(...)

```python
fname = Path(fnames[0])
```

**Verification:**
```python
assert fname.stem in rst
```

### Step 13: Assign img = image.imread(...)

```python
img = image.imread(fname)
```

### Step 14: Assign w = value

```python
w = img.shape[1]
```

### Step 15: Assign w0 = value

```python
w0 = size[0]
```

**Verification:**
```python
assert np.isclose(w, w0, atol=30) or np.isclose(w, w0 * 2, atol=30), f'w ∉ {{{w0}, {2 * w0}}}'
```


## Complete Example

```python
# Setup
# Fixtures: renderer_interactive_pyvistaqt, brain_gc, tmp_path

# Workflow
'Test a simple scraping example.'
pytest.importorskip('sphinx_gallery')
stc = read_source_estimate(fname_stc, subject='sample')
size = (600, 400)
brain = stc.plot(subjects_dir=subjects_dir, time_viewer=True, show_traces=True, hemi='split', size=size, views='lat')
fnames = [str(tmp_path / f'temp_{ii}.png') for ii in range(2)]
block_vars = dict(image_path_iterator=iter(fnames), example_globals=dict(brain=brain))
block = ('code', '', 1)
gallery_conf = dict(src_dir=str(tmp_path), compress_images=[], image_srcset=[], matplotlib_animations=(False, None))
scraper = _BrainScraper()
rst = scraper(block, block_vars, gallery_conf)
assert brain.plotter is None
assert brain._cleaned
del brain
fname = Path(fnames[0])
assert fname.stem in rst
assert fname.is_file()
img = image.imread(fname)
w = img.shape[1]
w0 = size[0]
assert np.isclose(w, w0, atol=30) or np.isclose(w, w0 * 2, atol=30), f'w ∉ {{{w0}, {2 * w0}}}'
```

## Next Steps


---

*Source: test_brain.py:1235 | Complexity: Advanced | Last updated: 2026-05-18*