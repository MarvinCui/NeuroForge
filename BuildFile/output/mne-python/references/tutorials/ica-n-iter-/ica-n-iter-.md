# How To: Ica N Iter 

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that ICA.n_iter_ is set after fitting.

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

### Step 1: 'Test that ICA.n_iter_ is set after fitting.'

```python
'Test that ICA.n_iter_ is set after fitting.'
```

**Verification:**
```python
assert ica.method == method
```

### Step 2: Call _skip_check_picard()

```python
_skip_check_picard(method)
```

**Verification:**
```python
assert_equal(ica.n_iter_, max_iter)
```

### Step 3: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname).crop(0.5, stop).load_data()
```

**Verification:**
```python
assert ica.method == method
```

### Step 4: Assign n_components = 3

```python
n_components = 3
```

**Verification:**
```python
assert_equal(ica.n_iter_, max_iter)
```

### Step 5: Assign max_iter = 1

```python
max_iter = 1
```

### Step 6: Assign ica = ICA(...)

```python
ica = ICA(n_components=n_components, max_iter=max_iter, method=method, random_state=0)
```

**Verification:**
```python
assert ica.method == method
```

### Step 7: Call assert_equal()

```python
assert_equal(ica.n_iter_, max_iter)
```

### Step 8: Assign output_fname = value

```python
output_fname = tmp_path / 'test_ica-ica.fif'
```

### Step 9: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica, raw.get_data('data'), limits=(5, 110))
```

### Step 10: Call ica.save()

```python
ica.save(output_fname)
```

### Step 11: Assign ica = read_ica(...)

```python
ica = read_ica(output_fname)
```

**Verification:**
```python
assert ica.method == method
```

### Step 12: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica)
```

### Step 13: Call assert_equal()

```python
assert_equal(ica.n_iter_, max_iter)
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
'Test that ICA.n_iter_ is set after fitting.'
_skip_check_picard(method)
raw = read_raw_fif(raw_fname).crop(0.5, stop).load_data()
n_components = 3
max_iter = 1
ica = ICA(n_components=n_components, max_iter=max_iter, method=method, random_state=0)
if method == 'infomax':
    ica.fit(raw)
else:
    with pytest.warns(UserWarning, match='did not converge'):
        ica.fit(raw)
assert ica.method == method
assert_equal(ica.n_iter_, max_iter)
output_fname = tmp_path / 'test_ica-ica.fif'
_assert_ica_attributes(ica, raw.get_data('data'), limits=(5, 110))
ica.save(output_fname)
ica = read_ica(output_fname)
assert ica.method == method
_assert_ica_attributes(ica)
assert_equal(ica.n_iter_, max_iter)
```

## Next Steps


---

*Source: test_ica.py:294 | Complexity: Advanced | Last updated: 2026-05-18*