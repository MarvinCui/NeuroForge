# How To: Order

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that order does not matter.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.cov`
- `mne.datasets`
- `mne.io`
- `mne.simulation`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that order does not matter.'

```python
'Test that order does not matter.'
```

**Verification:**
```python
assert 'meg' in evoked
```

### Step 2: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fwd_fname)
```

**Verification:**
```python
assert 'eeg' in evoked
```

### Step 3: Assign fwd = convert_forward_solution(...)

```python
fwd = convert_forward_solution(fwd, force_fixed=True, use_cps=False)
```

**Verification:**
```python
assert (eeg_picks > meg_picks.max()).all()
```

### Step 4: Assign evoked = unknown.pick(...)

```python
evoked = read_evokeds(ave_fname)[0].pick(['meg', 'eeg'])
```

**Verification:**
```python
assert_allclose(evoked_sim_2.data, want_data)
```

### Step 5: Assign meg_picks = pick_types(...)

```python
meg_picks = pick_types(evoked.info, meg=True)
```

### Step 6: Assign eeg_picks = pick_types(...)

```python
eeg_picks = pick_types(evoked.info, eeg=True)
```

**Verification:**
```python
assert (eeg_picks > meg_picks.max()).all()
```

### Step 7: Assign times = value

```python
times = np.arange(10) / 1000.0
```

### Step 8: Assign stc = simulate_sparse_stc(...)

```python
stc = simulate_sparse_stc(fwd['src'], 1, times=times, random_state=0)
```

### Step 9: Assign evoked_sim = simulate_evoked(...)

```python
evoked_sim = simulate_evoked(fwd, stc, evoked.info, nave=np.inf)
```

### Step 10: Assign reorder = np.concatenate(...)

```python
reorder = np.concatenate([eeg_picks, meg_picks])
```

### Step 11: Call evoked.reorder_channels()

```python
evoked.reorder_channels([evoked.ch_names[pick] for pick in reorder])
```

### Step 12: Assign evoked_sim_2 = simulate_evoked(...)

```python
evoked_sim_2 = simulate_evoked(fwd, stc, evoked.info, nave=np.inf)
```

### Step 13: Assign want_data = value

```python
want_data = evoked_sim.data[reorder]
```

### Step 14: Call assert_allclose()

```python
assert_allclose(evoked_sim_2.data, want_data)
```


## Complete Example

```python
# Workflow
'Test that order does not matter.'
fwd = read_forward_solution(fwd_fname)
fwd = convert_forward_solution(fwd, force_fixed=True, use_cps=False)
evoked = read_evokeds(ave_fname)[0].pick(['meg', 'eeg'])
assert 'meg' in evoked
assert 'eeg' in evoked
meg_picks = pick_types(evoked.info, meg=True)
eeg_picks = pick_types(evoked.info, eeg=True)
assert (eeg_picks > meg_picks.max()).all()
times = np.arange(10) / 1000.0
stc = simulate_sparse_stc(fwd['src'], 1, times=times, random_state=0)
evoked_sim = simulate_evoked(fwd, stc, evoked.info, nave=np.inf)
reorder = np.concatenate([eeg_picks, meg_picks])
evoked.reorder_channels([evoked.ch_names[pick] for pick in reorder])
evoked_sim_2 = simulate_evoked(fwd, stc, evoked.info, nave=np.inf)
want_data = evoked_sim.data[reorder]
assert_allclose(evoked_sim_2.data, want_data)
```

## Next Steps


---

*Source: test_evoked.py:173 | Complexity: Advanced | Last updated: 2026-05-18*