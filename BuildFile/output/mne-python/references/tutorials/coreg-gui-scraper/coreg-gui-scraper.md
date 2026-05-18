# How To: Coreg Gui Scraper

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the scrapper for the coregistration GUI.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `contextlib`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.utils`
- `mne.viz`
- `mne.gui`
- `mne.gui`
- `mne.gui`
- `mne.gui`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.gui`
- `mne.gui`
- `mne.gui`

**Setup Required:**
```python
# Fixtures: tmp_path, renderer_interactive_pyvistaqt
```

## Step-by-Step Guide

### Step 1: 'Test the scrapper for the coregistration GUI.'

```python
'Test the scrapper for the coregistration GUI.'
```

**Verification:**
```python
assert not image_path.is_file()
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sphinx_gallery')
```

**Verification:**
```python
assert not getattr(coreg, '_scraped', False)
```

### Step 3: Assign coreg = coregistration(...)

```python
coreg = coregistration(subject='sample', subjects_dir=subjects_dir, trans=fname_trans)
```

**Verification:**
```python
assert image_path.is_file()
```

### Step 4: Call unknown.mkdir()

```python
(tmp_path / '_images').mkdir()
```

**Verification:**
```python
assert coreg._scraped
```

### Step 5: Assign image_path = value

```python
image_path = tmp_path / '_images' / 'temp.png'
```

### Step 6: Assign gallery_conf = dict(...)

```python
gallery_conf = dict(builder_name='html', src_dir=tmp_path)
```

### Step 7: Assign block_vars = dict(...)

```python
block_vars = dict(example_globals=dict(gui=coreg), image_path_iterator=iter([str(image_path)]))
```

**Verification:**
```python
assert not image_path.is_file()
```

### Step 8: Call mne.gui._GUIScraper()

```python
mne.gui._GUIScraper()(None, block_vars, gallery_conf)
```

**Verification:**
```python
assert image_path.is_file()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, renderer_interactive_pyvistaqt

# Workflow
'Test the scrapper for the coregistration GUI.'
pytest.importorskip('sphinx_gallery')
from mne.gui import coregistration
coreg = coregistration(subject='sample', subjects_dir=subjects_dir, trans=fname_trans)
(tmp_path / '_images').mkdir()
image_path = tmp_path / '_images' / 'temp.png'
gallery_conf = dict(builder_name='html', src_dir=tmp_path)
block_vars = dict(example_globals=dict(gui=coreg), image_path_iterator=iter([str(image_path)]))
assert not image_path.is_file()
assert not getattr(coreg, '_scraped', False)
mne.gui._GUIScraper()(None, block_vars, gallery_conf)
assert image_path.is_file()
assert coreg._scraped
```

## Next Steps


---

*Source: test_coreg.py:322 | Complexity: Advanced | Last updated: 2026-05-18*