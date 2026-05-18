# How To: Qt Scraper

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test sphinx-gallery scraping of the browser.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os.path`
- `pytest`
- `mne`

**Setup Required:**
```python
# Fixtures: raw, pg_backend, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test sphinx-gallery scraping of the browser.'

```python
'Test sphinx-gallery scraping of the browser.'
```

**Verification:**
```python
assert not any((op.isfile(image_path) for image_path in image_paths))
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sphinx_gallery')
```

**Verification:**
```python
assert not getattr(fig, '_scraped', False)
```

### Step 3: Assign fig = raw.plot(...)

```python
fig = raw.plot(group_by='selection')
```

**Verification:**
```python
assert all((op.isfile(image_path) for image_path in image_paths))
```

### Step 4: Call unknown.mkdir()

```python
(tmp_path / '_images').mkdir()
```

**Verification:**
```python
assert fig._scraped
```

### Step 5: Assign image_paths = value

```python
image_paths = [str(tmp_path / '_images' / 'temp_{ii}.png') for ii in range(2)]
```

### Step 6: Assign gallery_conf = dict(...)

```python
gallery_conf = dict(builder_name='html', src_dir=str(tmp_path))
```

### Step 7: Assign block_vars = dict(...)

```python
block_vars = dict(example_globals=dict(fig=fig), image_path_iterator=iter(image_paths))
```

**Verification:**
```python
assert not any((op.isfile(image_path) for image_path in image_paths))
```

### Step 8: Call mne.viz._scraper._MNEQtBrowserScraper()

```python
mne.viz._scraper._MNEQtBrowserScraper()(None, block_vars, gallery_conf)
```

**Verification:**
```python
assert all((op.isfile(image_path) for image_path in image_paths))
```


## Complete Example

```python
# Setup
# Fixtures: raw, pg_backend, tmp_path

# Workflow
'Test sphinx-gallery scraping of the browser.'
pytest.importorskip('sphinx_gallery')
fig = raw.plot(group_by='selection')
(tmp_path / '_images').mkdir()
image_paths = [str(tmp_path / '_images' / 'temp_{ii}.png') for ii in range(2)]
gallery_conf = dict(builder_name='html', src_dir=str(tmp_path))
block_vars = dict(example_globals=dict(fig=fig), image_path_iterator=iter(image_paths))
assert not any((op.isfile(image_path) for image_path in image_paths))
assert not getattr(fig, '_scraped', False)
mne.viz._scraper._MNEQtBrowserScraper()(None, block_vars, gallery_conf)
assert all((op.isfile(image_path) for image_path in image_paths))
assert fig._scraped
```

## Next Steps


---

*Source: test_scraper.py:13 | Complexity: Advanced | Last updated: 2026-05-18*