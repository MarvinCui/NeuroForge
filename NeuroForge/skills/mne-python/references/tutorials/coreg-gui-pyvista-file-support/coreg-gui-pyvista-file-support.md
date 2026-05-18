# How To: Coreg Gui Pyvista File Support

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading supported files.

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
# Fixtures: inst_path, tmp_path, renderer_interactive_pyvistaqt
```

## Step-by-Step Guide

### Step 1: 'Test reading supported files.'

```python
'Test reading supported files.'
```

### Step 2: Assign coreg._accept_close_event = True

```python
coreg._accept_close_event = True
```

### Step 3: Call coreg.close()

```python
coreg.close()
```

### Step 4: Assign tmp_info = read_info(...)

```python
tmp_info = read_info(raw_path)
```

### Step 5: Assign eeg_chans = value

```python
eeg_chans = []
```

### Step 6: Assign dig = DigMontage(...)

```python
dig = DigMontage(dig=tmp_info['dig'], ch_names=eeg_chans)
```

### Step 7: Assign inst_path = value

```python
inst_path = tmp_path / 'tmp-dig.fif'
```

### Step 8: Call dig.save()

```python
dig.save(inst_path)
```

### Step 9: Assign ctx = pytest.warns(...)

```python
ctx = pytest.warns(RuntimeWarning, match='MEG ref channel RMSP')
```

### Step 10: Assign coreg = coregistration(...)

```python
coreg = coregistration(inst=inst_path, subject='sample', subjects_dir=subjects_dir)
```

### Step 11: Assign ctx = pytest.warns(...)

```python
ctx = pytest.warns(RuntimeWarning, match='assuming "head"')
```

### Step 12: Assign ctx = nullcontext(...)

```python
ctx = nullcontext()
```

### Step 13: Call eeg_chans.append()

```python
eeg_chans.append(f"EEG {pt['ident']:03d}")
```


## Complete Example

```python
# Setup
# Fixtures: inst_path, tmp_path, renderer_interactive_pyvistaqt

# Workflow
'Test reading supported files.'
from mne.gui import coregistration
if inst_path == 'gen_montage':
    tmp_info = read_info(raw_path)
    eeg_chans = []
    for pt in tmp_info['dig']:
        if pt['kind'] == FIFF.FIFFV_POINT_EEG:
            eeg_chans.append(f"EEG {pt['ident']:03d}")
    dig = DigMontage(dig=tmp_info['dig'], ch_names=eeg_chans)
    inst_path = tmp_path / 'tmp-dig.fif'
    dig.save(inst_path)
if inst_path == ctf_raw_path:
    ctx = pytest.warns(RuntimeWarning, match='MEG ref channel RMSP')
elif inst_path == snirf_nirsport2_raw_path:
    ctx = pytest.warns(RuntimeWarning, match='assuming "head"')
else:
    ctx = nullcontext()
with ctx:
    coreg = coregistration(inst=inst_path, subject='sample', subjects_dir=subjects_dir)
coreg._accept_close_event = True
coreg.close()
```

## Next Steps


---

*Source: test_coreg.py:86 | Complexity: Advanced | Last updated: 2026-05-18*