# How To: Nihon Duplicate Channels

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test deduplication of channel names.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `numpy.testing`
- `mne.datasets`
- `mne.io`
- `mne.io.nihon`
- `mne.io.nihon.nihon`
- `mne.io.tests.test_raw`

**Setup Required:**
```python
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test deduplication of channel names.'

```python
'Test deduplication of channel names.'
```

**Verification:**
```python
assert len(nihon._read_21e_file(fname)) > len(set(nihon._read_21e_file(fname)))
```

### Step 2: Assign fname = value

```python
fname = data_path / 'NihonKohden' / 'MB0400FU.EEG'
```

### Step 3: Call monkeypatch.setattr()

```python
monkeypatch.setattr(nihon, '_read_21e_file', return_channel_duplicates)
```

**Verification:**
```python
assert len(nihon._read_21e_file(fname)) > len(set(nihon._read_21e_file(fname)))
```

### Step 4: Assign msg = "Channel names are not unique, found duplicates for: {'FP1'}. Applying running numbers for duplicates."

```python
msg = "Channel names are not unique, found duplicates for: {'FP1'}. Applying running numbers for duplicates."
```

### Step 5: Assign ch_names = value

```python
ch_names = nihon._default_chan_labels
```

### Step 6: Assign unknown = value

```python
ch_names[1] = ch_names[0]
```

### Step 7: Call read_raw_nihon()

```python
read_raw_nihon(fname)
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
'Test deduplication of channel names.'
fname = data_path / 'NihonKohden' / 'MB0400FU.EEG'

def return_channel_duplicates(fname):
    ch_names = nihon._default_chan_labels
    ch_names[1] = ch_names[0]
    return ch_names
monkeypatch.setattr(nihon, '_read_21e_file', return_channel_duplicates)
assert len(nihon._read_21e_file(fname)) > len(set(nihon._read_21e_file(fname)))
msg = "Channel names are not unique, found duplicates for: {'FP1'}. Applying running numbers for duplicates."
with pytest.warns(RuntimeWarning, match=msg):
    read_raw_nihon(fname)
```

## Next Steps


---

*Source: test_nihon.py:75 | Complexity: Intermediate | Last updated: 2026-05-18*