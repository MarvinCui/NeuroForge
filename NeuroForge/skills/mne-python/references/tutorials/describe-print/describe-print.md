# How To: Describe Print

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test print output of describe method.

## Prerequisites

**Required Modules:**
- `math`
- `os`
- `re`
- `contextlib`
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne._fiff.utils`
- `mne.io`
- `mne.io.base`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test print output of describe method.'

```python
'Test print output of describe method.'
```

**Verification:**
```python
assert len(s) == 378
```

### Step 2: Assign fname = value

```python
fname = Path(__file__).parent / 'data' / 'test_raw.fif'
```

**Verification:**
```python
assert re.match('<Raw | test_raw.fif, 376 x 14400 (24\\.0 s), ~3\\.. MB, data not loaded>', s[0]) is not None, s[0]
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname)
```

**Verification:**
```python
assert s[1] == ' ch  name      type  unit         min         Q1     median         Q3        max'
```

### Step 4: Assign f = StringIO(...)

```python
f = StringIO()
```

**Verification:**
```python
assert s[2] == '  0  MEG 0113  GRAD  fT/cm    -221.80     -38.57      -9.64      19.29     414.67'
```

### Step 5: Assign s = f.getvalue.strip.split(...)

```python
s = f.getvalue().strip().split('\n')
```

**Verification:**
```python
assert s[-1] == '375  EOG 061   EOG   µV       -231.41     271.28     277.16     285.66     334.69'
```

### Step 6: Call raw.describe()

```python
raw.describe()
```


## Complete Example

```python
# Workflow
'Test print output of describe method.'
fname = Path(__file__).parent / 'data' / 'test_raw.fif'
raw = read_raw_fif(fname)
f = StringIO()
with redirect_stdout(f):
    raw.describe()
s = f.getvalue().strip().split('\n')
assert len(s) == 378
assert re.match('<Raw | test_raw.fif, 376 x 14400 (24\\.0 s), ~3\\.. MB, data not loaded>', s[0]) is not None, s[0]
assert s[1] == ' ch  name      type  unit         min         Q1     median         Q3        max'
assert s[2] == '  0  MEG 0113  GRAD  fT/cm    -221.80     -38.57      -9.64      19.29     414.67'
assert s[-1] == '375  EOG 061   EOG   µV       -231.41     271.28     277.16     285.66     334.69'
```

## Next Steps


---

*Source: test_raw.py:864 | Complexity: Intermediate | Last updated: 2026-05-18*