# How To: Clean Confounds Inputs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check several types of supported inputs.

## Prerequisites

**Required Modules:**
- `pathlib`
- `typing`
- `numpy`
- `pytest`
- `scipy.signal`
- `numpy`
- `numpy.testing`
- `pandas`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.signal`


## Step-by-Step Guide

### Step 1: 'Check several types of supported inputs.'

```python
'Check several types of supported inputs.'
```

### Step 2: Assign unknown = generate_signals(...)

```python
signals, _, confounds = generate_signals(n_features=41, n_confounds=3, length=20)
```

### Step 3: Assign current_dir = value

```python
current_dir = Path(__file__).parent
```

### Step 4: Assign filename1 = value

```python
filename1 = current_dir / 'data' / 'spm_confounds.txt'
```

### Step 5: Assign filename2 = value

```python
filename2 = current_dir / 'data' / 'confounds_with_header.csv'
```

### Step 6: Call clean()

```python
clean(signals, detrend=False, standardize=None, confounds=filename1)
```

### Step 7: Call clean()

```python
clean(signals, detrend=False, standardize=None, confounds=filename2)
```

### Step 8: Call clean()

```python
clean(signals, detrend=False, standardize=None, confounds=confounds[:, 1])
```

### Step 9: Assign confounds_df = read_csv(...)

```python
confounds_df = read_csv(filename2, sep='\t')
```

### Step 10: Call clean()

```python
clean(signals, detrend=False, standardize=None, confounds=confounds_df.values)
```

### Step 11: Call clean()

```python
clean(signals, detrend=False, standardize=None, confounds=confounds_df)
```

### Step 12: Assign list_signal = signals.tolist(...)

```python
list_signal = signals.tolist()
```

### Step 13: Call clean()

```python
clean(list_signal, standardize=None)
```

### Step 14: Call clean()

```python
clean(signals, detrend=False, standardize=None, confounds=[filename1, confounds[:, 0:2], filename2, confounds[:, 2]])
```


## Complete Example

```python
# Workflow
'Check several types of supported inputs.'
signals, _, confounds = generate_signals(n_features=41, n_confounds=3, length=20)
current_dir = Path(__file__).parent
filename1 = current_dir / 'data' / 'spm_confounds.txt'
filename2 = current_dir / 'data' / 'confounds_with_header.csv'
clean(signals, detrend=False, standardize=None, confounds=filename1)
clean(signals, detrend=False, standardize=None, confounds=filename2)
clean(signals, detrend=False, standardize=None, confounds=confounds[:, 1])
confounds_df = read_csv(filename2, sep='\t')
clean(signals, detrend=False, standardize=None, confounds=confounds_df.values)
clean(signals, detrend=False, standardize=None, confounds=confounds_df)
list_signal = signals.tolist()
clean(list_signal, standardize=None)
clean(signals, detrend=False, standardize=None, confounds=[filename1, confounds[:, 0:2], filename2, confounds[:, 2]])
```

## Next Steps


---

*Source: test_signal.py:893 | Complexity: Advanced | Last updated: 2026-05-18*