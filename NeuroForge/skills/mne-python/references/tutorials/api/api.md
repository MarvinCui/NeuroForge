# How To: Api

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test LCMV/DICS API equivalence.

## Prerequisites

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

**Required Fixtures:**
- `api_client` fixture


## Step-by-Step Guide

### Step 1: 'Test LCMV/DICS API equivalence.'

```python
'Test LCMV/DICS API equivalence.'
```

**Verification:**
```python
assert lcmv_names == dics_names
```

### Step 2: Assign lcmv_names = list(...)

```python
lcmv_names = list(signature(make_lcmv).parameters)
```

### Step 3: Assign dics_names = list(...)

```python
dics_names = list(signature(make_dics).parameters)
```

### Step 4: Assign unknown = 'data_cov'

```python
dics_names[dics_names.index('csd')] = 'data_cov'
```

### Step 5: Assign unknown = 'noise_cov'

```python
dics_names[dics_names.index('noise_csd')] = 'noise_cov'
```

### Step 6: Call dics_names.pop()

```python
dics_names.pop(dics_names.index('real_filter'))
```

**Verification:**
```python
assert lcmv_names == dics_names
```


## Complete Example

```python
# Workflow
'Test LCMV/DICS API equivalence.'
lcmv_names = list(signature(make_lcmv).parameters)
dics_names = list(signature(make_dics).parameters)
dics_names[dics_names.index('csd')] = 'data_cov'
dics_names[dics_names.index('noise_csd')] = 'noise_cov'
dics_names.pop(dics_names.index('real_filter'))
assert lcmv_names == dics_names
```

## Next Steps


---

*Source: test_lcmv.py:1266 | Complexity: Intermediate | Last updated: 2026-05-18*