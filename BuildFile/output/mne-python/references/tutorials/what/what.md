# How To: What

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test mne.what.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `glob`
- `pathlib`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, verbose_debug
```

## Step-by-Step Guide

### Step 1: 'Test mne.what.'

```python
'Test mne.what.'
```

**Verification:**
```python
assert what(fname) == 'ica'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert this == want_dict[kind], fname
```

### Step 3: Assign ica = ICA(...)

```python
ica = ICA(max_iter=1, random_state=0)
```

**Verification:**
```python
assert set(want_dict) == got
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(np.random.RandomState(0).randn(3, 10), create_info(3, 1000.0, 'eeg'))
```

**Verification:**
```python
assert what(fname) == 'unknown'
```

### Step 5: Assign fname = value

```python
fname = tmp_path / 'x-ica.fif'
```

### Step 6: Call ica.save()

```python
ica.save(fname)
```

**Verification:**
```python
assert what(fname) == 'ica'
```

### Step 7: Assign fnames = glob.glob(...)

```python
fnames = glob.glob(str(data_path / 'MEG' / 'sample' / '*.fif'))
```

### Step 8: Assign fnames = sorted(...)

```python
fnames = sorted(fnames)
```

### Step 9: Assign want_dict = dict(...)

```python
want_dict = dict(eve='events', ave='evoked', cov='cov', ica='ica', inv='inverse', fwd='forward', trans='transform', proj='proj', raw='raw', sol='bem solution', bem='bem surfaces', src='src', dense='bem surfaces', head='bem surfaces', fiducials='fiducials')
```

### Step 10: Assign got = set(...)

```python
got = set()
```

**Verification:**
```python
assert set(want_dict) == got
```

### Step 11: Assign fname = value

```python
fname = data_path / 'MEG' / 'sample' / 'sample_audvis-ave_xfit.dip'
```

**Verification:**
```python
assert what(fname) == 'unknown'
```

### Step 12: Call ica.fit()

```python
ica.fit(raw)
```

### Step 13: Call print()

```python
print(fname)
```

### Step 14: Assign kind = value

```python
kind = Path(fname).stem.split('-')[-1]
```

### Step 15: Assign this = what(...)

```python
this = what(fname)
```

**Verification:**
```python
assert this == want_dict[kind], fname
```

### Step 16: Call print()

```python
print()
```

### Step 17: Call got.add()

```python
got.add(kind)
```

### Step 18: Assign kind = value

```python
kind = kind.split('_')[-1]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, verbose_debug

# Workflow
'Test mne.what.'
pytest.importorskip('sklearn')
ica = ICA(max_iter=1, random_state=0)
raw = RawArray(np.random.RandomState(0).randn(3, 10), create_info(3, 1000.0, 'eeg'))
with _record_warnings():
    ica.fit(raw)
fname = tmp_path / 'x-ica.fif'
ica.save(fname)
assert what(fname) == 'ica'
fnames = glob.glob(str(data_path / 'MEG' / 'sample' / '*.fif'))
fnames += glob.glob(str(data_path / 'subjects' / 'sample' / 'bem' / '*.fif'))
fnames += [str(fname)]
fnames = sorted(fnames)
want_dict = dict(eve='events', ave='evoked', cov='cov', ica='ica', inv='inverse', fwd='forward', trans='transform', proj='proj', raw='raw', sol='bem solution', bem='bem surfaces', src='src', dense='bem surfaces', head='bem surfaces', fiducials='fiducials')
got = set()
for fname in fnames:
    print(fname)
    kind = Path(fname).stem.split('-')[-1]
    if len(kind) > 5:
        kind = kind.split('_')[-1]
    this = what(fname)
    assert this == want_dict[kind], fname
    print()
    got.add(kind)
assert set(want_dict) == got
fname = data_path / 'MEG' / 'sample' / 'sample_audvis-ave_xfit.dip'
assert what(fname) == 'unknown'
```

## Next Steps


---

*Source: test_what.py:22 | Complexity: Advanced | Last updated: 2026-05-18*