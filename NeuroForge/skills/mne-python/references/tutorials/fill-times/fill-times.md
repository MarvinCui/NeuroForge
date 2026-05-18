# How To: Fill Times

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test use of pd.merge_asof in _fill_times.

We are merging on floating
point values. pd.merge_asof is used so that any differences in floating
point precision between df['samples']['times'] and the times generated
with np.arange don't result in the time columns not merging
correctly - i.e. 1560687.0 and 1560687.000001 should merge.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.eyelink._utils`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: "Test use of pd.merge_asof in _fill_times.\n\n    We are merging on floating\n    point values. pd.merge_asof is used so that any differences in floating\n    point precision between df['samples']['times'] and the times generated\n    with np.arange don't result in the time columns not merging\n    correctly - i.e. 1560687.0 and 1560687.000001 should merge.\n    "

```python
"Test use of pd.merge_asof in _fill_times.\n\n    We are merging on floating\n    point values. pd.merge_asof is used so that any differences in floating\n    point precision between df['samples']['times'] and the times generated\n    with np.arange don't result in the time columns not merging\n    correctly - i.e. 1560687.0 and 1560687.000001 should merge.\n    "
```

**Verification:**
```python
assert not df['pupil_left'].isna().sum()
```

### Step 2: Assign raw = read_raw_eyelink(...)

```python
raw = read_raw_eyelink(fname, create_annotations=False)
```

**Verification:**
```python
assert df_merged['pupil_left'].isna().sum() == nan_count
```

### Step 3: Assign sfreq = value

```python
sfreq = raw.info['sfreq']
```

### Step 4: Assign df = value

```python
df = raw.to_data_frame()[:1000]
```

**Verification:**
```python
assert not df['pupil_left'].isna().sum()
```

### Step 5: Assign nan_count = unknown.isna.sum(...)

```python
nan_count = df['pupil_left'].isna().sum()
```

### Step 6: Assign df_merged = _adjust_times(...)

```python
df_merged = _adjust_times(df, sfreq)
```

**Verification:**
```python
assert df_merged['pupil_left'].isna().sum() == nan_count
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
"Test use of pd.merge_asof in _fill_times.\n\n    We are merging on floating\n    point values. pd.merge_asof is used so that any differences in floating\n    point precision between df['samples']['times'] and the times generated\n    with np.arange don't result in the time columns not merging\n    correctly - i.e. 1560687.0 and 1560687.000001 should merge.\n    "
raw = read_raw_eyelink(fname, create_annotations=False)
sfreq = raw.info['sfreq']
df = raw.to_data_frame()[:1000]
assert not df['pupil_left'].isna().sum()
nan_count = df['pupil_left'].isna().sum()
df_merged = _adjust_times(df, sfreq)
assert df_merged['pupil_left'].isna().sum() == nan_count
```

## Next Steps


---

*Source: test_eyelink.py:152 | Complexity: Intermediate | Last updated: 2026-05-18*