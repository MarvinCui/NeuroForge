# How To: Apply Function Verbose

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test apply function verbosity.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `mne`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test apply function verbosity.'

```python
'Test apply function verbosity.'
```

**Verification:**
```python
assert len(sio.getvalue(close=False)) == 0
```

### Step 2: Assign n_chan = 2

```python
n_chan = 2
```

**Verification:**
```python
assert out is raw
```

### Step 3: Assign n_times = 3

```python
n_times = 3
```

**Verification:**
```python
assert sio.getvalue().count('\n') == n_chan
```

### Step 4: Assign ch_names = value

```python
ch_names = [str(ii) for ii in range(n_chan)]
```

### Step 5: Assign raw = RawArray(...)

```python
raw = RawArray(np.zeros((n_chan, n_times)), create_info(ch_names, 1.0, 'mag'))
```

### Step 6: Call raw.apply_function()

```python
raw.apply_function(printer, channel_wise=False)
```

### Step 7: Call raw.apply_function()

```python
raw.apply_function(bad_1)
```

### Step 8: Call raw.apply_function()

```python
raw.apply_function(bad_2)
```

### Step 9: Call raw.apply_function()

```python
raw.apply_function(bad_1, n_jobs=2)
```

### Step 10: Call raw.apply_function()

```python
raw.apply_function(bad_2, n_jobs=2)
```

### Step 11: Call raw.apply_function()

```python
raw.apply_function(bad_1, channel_wise=False)
```

### Step 12: Call raw.apply_function()

```python
raw.apply_function(bad_3, channel_wise=False)
```

### Step 13: Assign out = raw.apply_function(...)

```python
out = raw.apply_function(printer, verbose=False)
```

**Verification:**
```python
assert len(sio.getvalue(close=False)) == 0
```

### Step 14: Call raw.apply_function()

```python
raw.apply_function(printer, verbose=True)
```

**Verification:**
```python
assert sio.getvalue().count('\n') == n_chan
```


## Complete Example

```python
# Workflow
'Test apply function verbosity.'
n_chan = 2
n_times = 3
ch_names = [str(ii) for ii in range(n_chan)]
raw = RawArray(np.zeros((n_chan, n_times)), create_info(ch_names, 1.0, 'mag'))
with pytest.raises(TypeError, match='Return value must be an ndarray'):
    raw.apply_function(bad_1)
with pytest.raises(ValueError, match='Return data must have shape'):
    raw.apply_function(bad_2)
with pytest.raises(TypeError, match='Return value must be an ndarray'):
    raw.apply_function(bad_1, n_jobs=2)
with pytest.raises(ValueError, match='Return data must have shape'):
    raw.apply_function(bad_2, n_jobs=2)
raw.apply_function(printer, channel_wise=False)
with pytest.raises(TypeError, match='Return value must be an ndarray'):
    raw.apply_function(bad_1, channel_wise=False)
with pytest.raises(ValueError, match='Return data must have shape'):
    raw.apply_function(bad_3, channel_wise=False)
with catch_logging() as sio:
    out = raw.apply_function(printer, verbose=False)
    assert len(sio.getvalue(close=False)) == 0
    assert out is raw
    raw.apply_function(printer, verbose=True)
    assert sio.getvalue().count('\n') == n_chan
```

## Next Steps


---

*Source: test_apply_function.py:35 | Complexity: Advanced | Last updated: 2026-05-18*