# How To: Fetch Atlas Pauli 2017

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test fetch atlas pauli 2017

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
# Fixtures: tmp_path, request_mocker
```

## Step-by-Step Guide

### Step 1: Assign labels = pd.DataFrame.to_csv(...)

```python
labels = pd.DataFrame({'label': [f'label_{i}' for i in range(16)]}).to_csv(sep='\t', header=False)
```

**Verification:**
```python
assert len(data.labels) == 17
```

### Step 2: Assign det_atlas = data_gen.generate_labeled_regions(...)

```python
det_atlas = data_gen.generate_labeled_regions((7, 6, 5), 16)
```

**Verification:**
```python
assert len(np.unique(values)) == 17
```

### Step 3: Assign unknown = data_gen.generate_maps(...)

```python
prob_atlas, _ = data_gen.generate_maps((7, 6, 5), 16)
```

**Verification:**
```python
assert load(data.maps).shape[-1] == 16
```

### Step 4: Assign unknown = labels

```python
request_mocker.url_mapping['*osf.io/6qrcb/*'] = labels
```

### Step 5: Assign unknown = det_atlas

```python
request_mocker.url_mapping['*osf.io/5mqfx/*'] = det_atlas
```

### Step 6: Assign unknown = prob_atlas

```python
request_mocker.url_mapping['*osf.io/w8zq2/*'] = prob_atlas
```

### Step 7: Assign data_dir = str(...)

```python
data_dir = str(tmp_path / 'pauli_2017')
```

### Step 8: Assign data = fetch_atlas_pauli_2017(...)

```python
data = fetch_atlas_pauli_2017('deterministic', data_dir)
```

### Step 9: Call validate_atlas()

```python
validate_atlas(data)
```

**Verification:**
```python
assert len(data.labels) == 17
```

### Step 10: Assign values = get_data(...)

```python
values = get_data(load(data.maps))
```

**Verification:**
```python
assert len(np.unique(values)) == 17
```

### Step 11: Assign data = fetch_atlas_pauli_2017(...)

```python
data = fetch_atlas_pauli_2017('probabilistic', data_dir)
```

### Step 12: Call validate_atlas()

```python
validate_atlas(data)
```

**Verification:**
```python
assert load(data.maps).shape[-1] == 16
```

### Step 13: Call fetch_atlas_pauli_2017()

```python
fetch_atlas_pauli_2017(atlas_type='junk for testing', data_dir=data_dir)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker

# Workflow
labels = pd.DataFrame({'label': [f'label_{i}' for i in range(16)]}).to_csv(sep='\t', header=False)
det_atlas = data_gen.generate_labeled_regions((7, 6, 5), 16)
prob_atlas, _ = data_gen.generate_maps((7, 6, 5), 16)
request_mocker.url_mapping['*osf.io/6qrcb/*'] = labels
request_mocker.url_mapping['*osf.io/5mqfx/*'] = det_atlas
request_mocker.url_mapping['*osf.io/w8zq2/*'] = prob_atlas
data_dir = str(tmp_path / 'pauli_2017')
data = fetch_atlas_pauli_2017('deterministic', data_dir)
validate_atlas(data)
assert len(data.labels) == 17
values = get_data(load(data.maps))
assert len(np.unique(values)) == 17
data = fetch_atlas_pauli_2017('probabilistic', data_dir)
validate_atlas(data)
assert load(data.maps).shape[-1] == 16
with pytest.raises(ValueError, match="'atlas_type' must be one of"):
    fetch_atlas_pauli_2017(atlas_type='junk for testing', data_dir=data_dir)
```

## Next Steps


---

*Source: test_atlas.py:761 | Complexity: Advanced | Last updated: 2026-05-18*