# How To: To Data Frame Time Format

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test time conversion in evoked Pandas exporter.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pickle`
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.constants`
- `mne.evoked`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: time_format
```

## Step-by-Step Guide

### Step 1: 'Test time conversion in evoked Pandas exporter.'

```python
'Test time conversion in evoked Pandas exporter.'
```

**Verification:**
```python
assert isinstance(df['time'].iloc[0], dtypes[time_format])
```

### Step 2: Assign pd = pytest.importorskip(...)

```python
pd = pytest.importorskip('pandas')
```

### Step 3: Assign ave = read_evokeds(...)

```python
ave = read_evokeds(fname, 0)
```

### Step 4: Assign df = ave.to_data_frame(...)

```python
df = ave.to_data_frame(time_format=time_format)
```

### Step 5: Assign dtypes = value

```python
dtypes = {None: np.float64, 'ms': np.int64, 'timedelta': pd.Timedelta}
```

**Verification:**
```python
assert isinstance(df['time'].iloc[0], dtypes[time_format])
```


## Complete Example

```python
# Setup
# Fixtures: time_format

# Workflow
'Test time conversion in evoked Pandas exporter.'
pd = pytest.importorskip('pandas')
ave = read_evokeds(fname, 0)
df = ave.to_data_frame(time_format=time_format)
dtypes = {None: np.float64, 'ms': np.int64, 'timedelta': pd.Timedelta}
assert isinstance(df['time'].iloc[0], dtypes[time_format])
```

## Next Steps


---

*Source: test_evoked.py:481 | Complexity: Intermediate | Last updated: 2026-05-18*