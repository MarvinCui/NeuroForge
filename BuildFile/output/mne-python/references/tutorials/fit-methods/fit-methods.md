# How To: Fit Methods

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test fit_params for ICA.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.cov`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.io.eeglab.eeglab`
- `mne.preprocessing`
- `mne.preprocessing`
- `mne.preprocessing.ica`
- `mne.rank`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: method, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test fit_params for ICA.'

```python
'Test fit_params for ICA.'
```

**Verification:**
```python
assert fit_params == {}
```

### Step 2: Call _skip_check_picard()

```python
_skip_check_picard(method)
```

**Verification:**
```python
assert ica.fit_params == fit_params_after_instantiation
```

### Step 3: Assign fit_params = value

```python
fit_params = {}
```

### Step 4: Call ICA()

```python
ICA(fit_params=fit_params, method=method)
```

**Verification:**
```python
assert fit_params == {}
```

### Step 5: Assign output_fname = value

```python
output_fname = tmp_path / 'test_ica-ica.fif'
```

### Step 6: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(0.5, stop).load_data()
```

### Step 7: Assign n_components = 3

```python
n_components = 3
```

### Step 8: Assign max_iter = 1

```python
max_iter = 1
```

### Step 9: Assign fit_params = dict(...)

```python
fit_params = dict(extended=True)
```

### Step 10: Assign ica = ICA(...)

```python
ica = ICA(fit_params=fit_params, n_components=n_components, max_iter=max_iter, method=method)
```

### Step 11: Assign fit_params_after_instantiation = value

```python
fit_params_after_instantiation = ica.fit_params
```

### Step 12: Call ica.save()

```python
ica.save(output_fname)
```

### Step 13: Assign ica = read_ica(...)

```python
ica = read_ica(output_fname)
```

**Verification:**
```python
assert ica.fit_params == fit_params_after_instantiation
```

### Step 14: Call ica.fit()

```python
ica.fit(raw)
```

### Step 15: Call ica.fit()

```python
ica.fit(raw)
```


## Complete Example

```python
# Setup
# Fixtures: method, tmp_path

# Workflow
'Test fit_params for ICA.'
_skip_check_picard(method)
fit_params = {}
ICA(fit_params=fit_params, method=method)
assert fit_params == {}
if method in ['picard', 'infomax']:
    output_fname = tmp_path / 'test_ica-ica.fif'
    raw = read_raw_fif(raw_fname).crop(0.5, stop).load_data()
    n_components = 3
    max_iter = 1
    fit_params = dict(extended=True)
    ica = ICA(fit_params=fit_params, n_components=n_components, max_iter=max_iter, method=method)
    fit_params_after_instantiation = ica.fit_params
    if method == 'infomax':
        ica.fit(raw)
    else:
        with pytest.warns(UserWarning, match='did not converge'):
            ica.fit(raw)
    ica.save(output_fname)
    ica = read_ica(output_fname)
    assert ica.fit_params == fit_params_after_instantiation
```

## Next Steps


---

*Source: test_ica.py:1210 | Complexity: Advanced | Last updated: 2026-05-18*