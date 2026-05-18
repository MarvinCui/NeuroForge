# How To: Plot Overlapping Epochs With Events

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test drawing of event lines in overlapping epochs.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.event`
- `mne.utils`
- `mne.viz`

**Setup Required:**
```python
# Fixtures: browser_backend, event_id, expected_texts
```

## Step-by-Step Guide

### Step 1: 'Test drawing of event lines in overlapping epochs.'

```python
'Test drawing of event lines in overlapping epochs.'
```

**Verification:**
```python
assert len(lines) == len(epochs) * len(events)
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros(shape=(3, 2, 100))
```

**Verification:**
```python
assert set(texts) == expected_texts
```

### Step 3: Assign sfreq = 100

```python
sfreq = 100
```

**Verification:**
```python
assert len(lines) == len(events)
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(ch_names=('a', 'b'), ch_types=('misc', 'misc'), sfreq=sfreq)
```

**Verification:**
```python
assert set(texts) == expected_texts
```

### Step 5: Assign events = np.column_stack(...)

```python
events = np.column_stack(([40, 50, 60], [0, 0, 0], [1, 2, 3]))
```

### Step 6: Assign epochs = EpochsArray(...)

```python
epochs = EpochsArray(data, info, tmin=-0.4, events=events, event_id=dict(a=1, b=2, c=3))
```

### Step 7: Assign fig = epochs.plot(...)

```python
fig = epochs.plot(events=events, picks='misc', event_id=event_id)
```

### Step 8: Assign unknown = _get_event_lines_and_texts(...)

```python
lines, texts = _get_event_lines_and_texts(fig)
```

**Verification:**
```python
assert len(lines) == len(epochs) * len(events)
```

### Step 9: Assign events = np.vstack(...)

```python
events = np.vstack(([[0, 0, 4]], events[[0]], [[99, 0, 4]]))
```

### Step 10: Assign fig = unknown.plot(...)

```python
fig = epochs[0].plot(events=events, picks='misc', event_id=event_id)
```

### Step 11: Call expected_texts.add()

```python
expected_texts.add('4')
```

### Step 12: Assign unknown = _get_event_lines_and_texts(...)

```python
lines, texts = _get_event_lines_and_texts(fig)
```

**Verification:**
```python
assert len(lines) == len(events)
```

### Step 13: Call expected_texts.discard()

```python
expected_texts.discard(text)
```

**Verification:**
```python
assert set(texts) == expected_texts
```


## Complete Example

```python
# Setup
# Fixtures: browser_backend, event_id, expected_texts

# Workflow
'Test drawing of event lines in overlapping epochs.'
data = np.zeros(shape=(3, 2, 100))
sfreq = 100
info = create_info(ch_names=('a', 'b'), ch_types=('misc', 'misc'), sfreq=sfreq)
events = np.column_stack(([40, 50, 60], [0, 0, 0], [1, 2, 3]))
epochs = EpochsArray(data, info, tmin=-0.4, events=events, event_id=dict(a=1, b=2, c=3))
fig = epochs.plot(events=events, picks='misc', event_id=event_id)
lines, texts = _get_event_lines_and_texts(fig)
assert len(lines) == len(epochs) * len(events)
if browser_backend.name == 'matplotlib':
    assert set(texts) == expected_texts
events = np.vstack(([[0, 0, 4]], events[[0]], [[99, 0, 4]]))
fig = epochs[0].plot(events=events, picks='misc', event_id=event_id)
expected_texts.add('4')
for text in ('2', '3', 'b', 'c'):
    expected_texts.discard(text)
lines, texts = _get_event_lines_and_texts(fig)
assert len(lines) == len(events)
if browser_backend.name == 'matplotlib':
    assert set(texts) == expected_texts
```

## Next Steps


---

*Source: test_epochs.py:228 | Complexity: Advanced | Last updated: 2026-05-18*