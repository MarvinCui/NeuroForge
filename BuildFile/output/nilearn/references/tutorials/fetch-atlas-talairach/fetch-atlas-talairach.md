# How To: Fetch Atlas Talairach

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test fetch atlas talairach

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `re`
- `xml.etree.ElementTree`
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils`
- `nilearn._utils`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.datasets._utils`
- `nilearn.datasets.atlas`
- `nilearn.datasets.tests._testing`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path, request_mocker, capsys
```

## Step-by-Step Guide

### Step 1: Assign unknown = _get_small_fake_talairach(...)

```python
request_mocker.url_mapping['*talairach.nii'] = _get_small_fake_talairach()
```

**Verification:**
```python
assert_array_equal(get_data(talairach.maps).ravel(), level_values.T.ravel())
```

### Step 2: Assign level_values = value

```python
level_values = np.ones((81, 3)) * [0, 1, 2]
```

**Verification:**
```python
assert_array_equal(talairach.labels, ['Background', 'b', 'a'])
```

### Step 3: Assign talairach = fetch_atlas_talairach(...)

```python
talairach = fetch_atlas_talairach('hemisphere', data_dir=tmp_path)
```

**Verification:**
```python
assert_array_equal(get_data(talairach.maps).ravel(), level_values.ravel())
```

### Step 4: Call validate_atlas()

```python
validate_atlas(talairach)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(get_data(talairach.maps).ravel(), level_values.T.ravel())
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(talairach.labels, ['Background', 'b', 'a'])
```

### Step 7: Assign talairach = fetch_atlas_talairach(...)

```python
talairach = fetch_atlas_talairach('ba', data_dir=tmp_path)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(get_data(talairach.maps).ravel(), level_values.ravel())
```

### Step 9: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(fetch_atlas_talairach, capsys, level_name='hemisphere', data_dir=tmp_path)
```

### Step 10: Call fetch_atlas_talairach()

```python
fetch_atlas_talairach('bad_level')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker, capsys

# Workflow
request_mocker.url_mapping['*talairach.nii'] = _get_small_fake_talairach()
level_values = np.ones((81, 3)) * [0, 1, 2]
talairach = fetch_atlas_talairach('hemisphere', data_dir=tmp_path)
validate_atlas(talairach)
assert_array_equal(get_data(talairach.maps).ravel(), level_values.T.ravel())
assert_array_equal(talairach.labels, ['Background', 'b', 'a'])
talairach = fetch_atlas_talairach('ba', data_dir=tmp_path)
assert_array_equal(get_data(talairach.maps).ravel(), level_values.ravel())
with pytest.raises(ValueError):
    fetch_atlas_talairach('bad_level')
check_fetcher_verbosity(fetch_atlas_talairach, capsys, level_name='hemisphere', data_dir=tmp_path)
```

## Next Steps


---

*Source: test_atlas.py:734 | Complexity: Advanced | Last updated: 2026-05-18*