# How To: Plot Ica Scores

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting of ICA scores.

## Prerequisites

**Required Modules:**
- `sys`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`
- `mne.viz.ica`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test plotting of ICA scores.'

```python
'Test plotting of ICA scores.'
```

**Verification:**
```python
assert 2 == _get_geometry(fig)[1]
```

### Step 2: Assign raw = _get_raw(...)

```python
raw = _get_raw()
```

**Verification:**
```python
assert 1 == _get_geometry(fig)[1]
```

### Step 3: Assign picks = _get_picks(...)

```python
picks = _get_picks(raw)
```

**Verification:**
```python
assert 1 == _get_geometry(fig)[1]
```

### Step 4: Assign ica = ICA(...)

```python
ica = ICA(noise_cov=read_cov(cov_fname), n_components=2)
```

### Step 5: Call ica.plot_scores()

```python
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], figsize=(6.4, 2.7))
```

### Step 6: Call ica.plot_scores()

```python
ica.plot_scores([[0.3, 0.2], [0.3, 0.2]], axhline=[0.1, -0.1])
```

### Step 7: Assign ica.labels_ = dict(...)

```python
ica.labels_ = dict()
```

### Step 8: Assign unknown = 0

```python
ica.labels_['eog'] = 0
```

### Step 9: Assign unknown = 1

```python
ica.labels_['ecg'] = 1
```

### Step 10: Call ica.plot_scores()

```python
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='eog')
```

### Step 11: Call ica.plot_scores()

```python
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='ecg')
```

### Step 12: Assign unknown = 0

```python
ica.labels_['eog/0/foo'] = 0
```

### Step 13: Assign unknown = 0

```python
ica.labels_['ecg/1/bar'] = 0
```

### Step 14: Call ica.plot_scores()

```python
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='foo')
```

### Step 15: Call ica.plot_scores()

```python
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='eog')
```

### Step 16: Call ica.plot_scores()

```python
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='ecg')
```

### Step 17: Assign fig = ica.plot_scores(...)

```python
fig = ica.plot_scores([[0.3, 0.2], [0.3, 0.2], [0.3, 0.2]], axhline=[0.1, -0.1])
```

**Verification:**
```python
assert 2 == _get_geometry(fig)[1]
```

### Step 18: Assign fig = ica.plot_scores(...)

```python
fig = ica.plot_scores([[0.3, 0.2], [0.3, 0.2]], axhline=[0.1, -0.1], n_cols=1)
```

**Verification:**
```python
assert 1 == _get_geometry(fig)[1]
```

### Step 19: Assign fig = ica.plot_scores(...)

```python
fig = ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], n_cols=2)
```

**Verification:**
```python
assert 1 == _get_geometry(fig)[1]
```

### Step 20: Call ica.fit()

```python
ica.fit(raw, picks=picks)
```

### Step 21: Call ica.plot_scores()

```python
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels=['one', 'one-too-many'])
```

### Step 22: Call ica.plot_scores()

```python
ica.plot_scores([0.2])
```


## Complete Example

```python
# Workflow
'Test plotting of ICA scores.'
raw = _get_raw()
picks = _get_picks(raw)
ica = ICA(noise_cov=read_cov(cov_fname), n_components=2)
with pytest.warns(RuntimeWarning, match='projection'):
    ica.fit(raw, picks=picks)
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], figsize=(6.4, 2.7))
ica.plot_scores([[0.3, 0.2], [0.3, 0.2]], axhline=[0.1, -0.1])
ica.labels_ = dict()
ica.labels_['eog'] = 0
ica.labels_['ecg'] = 1
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='eog')
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='ecg')
ica.labels_['eog/0/foo'] = 0
ica.labels_['ecg/1/bar'] = 0
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='foo')
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='eog')
ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels='ecg')
fig = ica.plot_scores([[0.3, 0.2], [0.3, 0.2], [0.3, 0.2]], axhline=[0.1, -0.1])
assert 2 == _get_geometry(fig)[1]
fig = ica.plot_scores([[0.3, 0.2], [0.3, 0.2]], axhline=[0.1, -0.1], n_cols=1)
assert 1 == _get_geometry(fig)[1]
fig = ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], n_cols=2)
assert 1 == _get_geometry(fig)[1]
with pytest.raises(ValueError, match='Need as many'):
    ica.plot_scores([0.3, 0.2], axhline=[0.1, -0.1], labels=['one', 'one-too-many'])
with pytest.raises(ValueError, match='The length of'):
    ica.plot_scores([0.2])
```

## Next Steps


---

*Source: test_ica.py:521 | Complexity: Advanced | Last updated: 2026-05-18*