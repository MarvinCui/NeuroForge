# How To: Rescale

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test rescale.

## Prerequisites

**Required Modules:**
- `pickle`
- `copy`
- `datetime`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `scipy.signal`
- `numpy.fft`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne._fiff.write`
- `mne.annotations`
- `mne.baseline`
- `mne.chpi`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas`


## Step-by-Step Guide

### Step 1: 'Test rescale.'

```python
'Test rescale.'
```

**Verification:**
```python
assert_allclose(tester(mode='mean'), [-1, 0, 1, 2])
```

### Step 2: Assign data = np.array(...)

```python
data = np.array([2, 3, 4, 5], float)
```

**Verification:**
```python
assert_allclose(tester(mode='ratio'), data / 3.0)
```

### Step 3: Assign times = np.array(...)

```python
times = np.array([0, 1, 2, 3], float)
```

**Verification:**
```python
assert_allclose(tester(mode='logratio'), np.log10(data / 3.0))
```

### Step 4: Assign baseline = value

```python
baseline = (0, 2)
```

**Verification:**
```python
assert_allclose(tester(mode='percent'), (data - 3) / 3.0)
```

### Step 5: Assign tester = partial(...)

```python
tester = partial(rescale, data=data, times=times, baseline=baseline)
```

**Verification:**
```python
assert_allclose(tester(mode='zscore'), (data - 3) / np.std([2, 3, 4]))
```

### Step 6: Call assert_allclose()

```python
assert_allclose(tester(mode='mean'), [-1, 0, 1, 2])
```

**Verification:**
```python
assert_allclose(tester(mode='zlogratio'), x / s)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(tester(mode='ratio'), data / 3.0)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(tester(mode='logratio'), np.log10(data / 3.0))
```

### Step 9: Call assert_allclose()

```python
assert_allclose(tester(mode='percent'), (data - 3) / 3.0)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(tester(mode='zscore'), (data - 3) / np.std([2, 3, 4]))
```

### Step 11: Assign x = value

```python
x = data / 3.0
```

### Step 12: Assign x = np.log10(...)

```python
x = np.log10(x)
```

### Step 13: Assign s = np.std(...)

```python
s = np.std(x[:3])
```

### Step 14: Call assert_allclose()

```python
assert_allclose(tester(mode='zlogratio'), x / s)
```


## Complete Example

```python
# Workflow
'Test rescale.'
data = np.array([2, 3, 4, 5], float)
times = np.array([0, 1, 2, 3], float)
baseline = (0, 2)
tester = partial(rescale, data=data, times=times, baseline=baseline)
assert_allclose(tester(mode='mean'), [-1, 0, 1, 2])
assert_allclose(tester(mode='ratio'), data / 3.0)
assert_allclose(tester(mode='logratio'), np.log10(data / 3.0))
assert_allclose(tester(mode='percent'), (data - 3) / 3.0)
assert_allclose(tester(mode='zscore'), (data - 3) / np.std([2, 3, 4]))
x = data / 3.0
x = np.log10(x)
s = np.std(x[:3])
assert_allclose(tester(mode='zlogratio'), x / s)
```

## Next Steps


---

*Source: test_epochs.py:1096 | Complexity: Advanced | Last updated: 2026-05-18*