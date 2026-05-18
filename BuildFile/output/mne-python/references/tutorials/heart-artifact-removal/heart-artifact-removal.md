# How To: Heart Artifact Removal

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test PCA-OBS analysis and heart artifact removal of ECG datasets.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `mne.io`
- `mne.io.fiff.raw`
- `mne.preprocessing`

**Setup Required:**
```python
# Fixtures: short_raw_data
```

## Step-by-Step Guide

### Step 1: 'Test PCA-OBS analysis and heart artifact removal of ECG datasets.'

```python
'Test PCA-OBS analysis and heart artifact removal of ECG datasets.'
```

### Step 2: Assign pd = pytest.importorskip(...)

```python
pd = pytest.importorskip('pandas')
```

### Step 3: Assign ecg_event_times = value

```python
ecg_event_times = np.linspace(0, orig_df['time'].iloc[-1], 20)[1:-1]
```

### Step 4: Assign short_raw_data = apply_pca_obs(...)

```python
short_raw_data = apply_pca_obs(raw=short_raw_data, picks=['eeg'], qrs_times=ecg_event_times, n_jobs=1)
```

### Step 5: Call pd.testing.assert_index_equal()

```python
pd.testing.assert_index_equal(orig_df.columns, removed_heart_artifact_df.columns)
```

### Step 6: Assign altered_cols = value

```python
altered_cols = [c for c in orig_df.columns if c.startswith('EEG')]
```

### Step 7: Assign unaltered_cols = value

```python
unaltered_cols = [c for c in orig_df.columns if not c.startswith('EEG')]
```

### Step 8: Call pd.testing.assert_frame_equal()

```python
pd.testing.assert_frame_equal(orig_df[unaltered_cols], removed_heart_artifact_df[unaltered_cols])
```

### Step 9: Call pd.testing.assert_series_equal()

```python
pd.testing.assert_series_equal(orig_df[col], removed_heart_artifact_df[col])
```


## Complete Example

```python
# Setup
# Fixtures: short_raw_data

# Workflow
'Test PCA-OBS analysis and heart artifact removal of ECG datasets.'
pd = pytest.importorskip('pandas')
orig_df: pd.DataFrame = short_raw_data.to_data_frame().copy(deep=True)
ecg_event_times = np.linspace(0, orig_df['time'].iloc[-1], 20)[1:-1]
short_raw_data = apply_pca_obs(raw=short_raw_data, picks=['eeg'], qrs_times=ecg_event_times, n_jobs=1)
removed_heart_artifact_df: pd.DataFrame = short_raw_data.to_data_frame()
pd.testing.assert_index_equal(orig_df.columns, removed_heart_artifact_df.columns)
altered_cols = [c for c in orig_df.columns if c.startswith('EEG')]
for col in altered_cols:
    with pytest.raises(AssertionError):
        pd.testing.assert_series_equal(orig_df[col], removed_heart_artifact_df[col])
unaltered_cols = [c for c in orig_df.columns if not c.startswith('EEG')]
pd.testing.assert_frame_equal(orig_df[unaltered_cols], removed_heart_artifact_df[unaltered_cols])
```

## Next Steps


---

*Source: test_pca_obs.py:24 | Complexity: Advanced | Last updated: 2026-05-18*