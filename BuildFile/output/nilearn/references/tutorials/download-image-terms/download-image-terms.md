# How To: Download Image Terms

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test _download_image_terms.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `hashlib`
- `json`
- `os`
- `re`
- `stat`
- `pathlib`
- `urllib`
- `numpy`
- `pandas`
- `pytest`
- `requests`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path, request_mocker
```

## Step-by-Step Guide

### Step 1: 'Test _download_image_terms.'

```python
'Test _download_image_terms.'
```

### Step 2: Assign image_info = value

```python
image_info = {'id': 'a'}
```

### Step 3: Assign collection = value

```python
collection = {'relative_path': 'collection', 'absolute_path': tmp_path / 'collection'}
```

### Step 4: Call unknown.mkdir()

```python
collection['absolute_path'].mkdir(parents=True)
```

### Step 5: Assign download_params = value

```python
download_params = {'temp_dir': tmp_path, 'verbose': 3, 'fetch_neurosynth_words': True}
```

### Step 6: Assign unknown = requests.RequestException(...)

```python
request_mocker.url_mapping['*'] = requests.RequestException()
```

### Step 7: Call neurovault._download_image_terms()

```python
neurovault._download_image_terms(image_info, collection, download_params)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker

# Workflow
'Test _download_image_terms.'
image_info = {'id': 'a'}
collection = {'relative_path': 'collection', 'absolute_path': tmp_path / 'collection'}
collection['absolute_path'].mkdir(parents=True)
download_params = {'temp_dir': tmp_path, 'verbose': 3, 'fetch_neurosynth_words': True}
request_mocker.url_mapping['*'] = requests.RequestException()
neurovault._download_image_terms(image_info, collection, download_params)
```

## Next Steps


---

*Source: test_neurovault.py:724 | Complexity: Intermediate | Last updated: 2026-05-18*