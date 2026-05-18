# How To: Lcmv Maxfiltered

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test LCMV on maxfiltered data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `copy`
- `inspect`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `scipy.spatial.distance`
- `mne`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne.beamformer`
- `mne.beamformer._compute_beamformer`
- `mne.datasets`
- `mne.fixes`
- `mne.minimum_norm`
- `mne.minimum_norm.tests.test_inverse`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: mf_data, use_rank
```

## Step-by-Step Guide

### Step 1: 'Test LCMV on maxfiltered data.'

```python
'Test LCMV on maxfiltered data.'
```

**Verification:**
```python
assert rank == {'mag': 71}
```

### Step 2: Assign unknown = mf_data

```python
epochs, data_cov, fwd = mf_data
```

**Verification:**
```python
assert f"Making LCMV beamformer with rank {{'mag': {n}}}" in log
```

### Step 3: Assign rank = compute_rank(...)

```python
rank = compute_rank(data_cov, info=epochs.info)
```

**Verification:**
```python
assert rank == {'mag': 71}
```

### Step 4: Assign ctx = nullcontext(...)

```python
ctx = nullcontext()
```

### Step 5: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

### Step 6: Assign n = value

```python
n = 102 if use_rank == 'full' else 71
```

**Verification:**
```python
assert f"Making LCMV beamformer with rank {{'mag': {n}}}" in log
```

### Step 7: Assign use_rank = rank

```python
use_rank = rank
```

### Step 8: Call make_lcmv()

```python
make_lcmv(epochs.info, fwd, data_cov, rank=use_rank, verbose=True)
```

### Step 9: Assign ctx = pytest.warns(...)

```python
ctx = pytest.warns(RuntimeWarning, match='rank as it exceeds')
```


## Complete Example

```python
# Setup
# Fixtures: mf_data, use_rank

# Workflow
'Test LCMV on maxfiltered data.'
epochs, data_cov, fwd = mf_data
rank = compute_rank(data_cov, info=epochs.info)
assert rank == {'mag': 71}
ctx = nullcontext()
if use_rank == 'computed':
    use_rank = rank
elif use_rank is None:
    ctx = pytest.warns(RuntimeWarning, match='rank as it exceeds')
with catch_logging() as log, ctx:
    make_lcmv(epochs.info, fwd, data_cov, rank=use_rank, verbose=True)
log = log.getvalue()
n = 102 if use_rank == 'full' else 71
assert f"Making LCMV beamformer with rank {{'mag': {n}}}" in log
```

## Next Steps


---

*Source: test_lcmv.py:1115 | Complexity: Advanced | Last updated: 2026-05-18*