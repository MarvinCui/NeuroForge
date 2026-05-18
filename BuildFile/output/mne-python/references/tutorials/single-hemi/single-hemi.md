# How To: Single Hemi

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test single hemi support.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `platform`
- `contextlib`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `matplotlib`
- `matplotlib.lines`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.utils`
- `mne.viz`
- `mne.viz._brain`
- `mne.viz._brain.colormap`
- `mne.viz.utils`
- `mne.viz._brain`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: hemi, renderer_interactive_pyvistaqt, brain_gc
```

## Step-by-Step Guide

### Step 1: 'Test single hemi support.'

```python
'Test single hemi support.'
```

### Step 2: Assign stc = read_source_estimate(...)

```python
stc = read_source_estimate(fname_stc)
```

### Step 3: Assign unknown = value

```python
idx, order = (0, 1) if hemi == 'lh' else (1, -1)
```

### Step 4: Assign stc = SourceEstimate(...)

```python
stc = SourceEstimate(getattr(stc, f'{hemi}_data'), [stc.vertices[idx], []][::order], 0, 1, 'sample')
```

### Step 5: Assign brain = stc.plot(...)

```python
brain = stc.plot(subjects_dir=subjects_dir, hemi='both', size=300, cortex='0.5')
```

### Step 6: Call brain.close()

```python
brain.close()
```

### Step 7: Assign unknown = np.array(...)

```python
stc.vertices[1 - idx] = np.array([])
```

### Step 8: Assign brain = stc.plot(...)

```python
brain = stc.plot(subjects_dir=subjects_dir, hemi=hemi, size=300)
```

### Step 9: Call brain.close()

```python
brain.close()
```


## Complete Example

```python
# Setup
# Fixtures: hemi, renderer_interactive_pyvistaqt, brain_gc

# Workflow
'Test single hemi support.'
stc = read_source_estimate(fname_stc)
idx, order = (0, 1) if hemi == 'lh' else (1, -1)
stc = SourceEstimate(getattr(stc, f'{hemi}_data'), [stc.vertices[idx], []][::order], 0, 1, 'sample')
brain = stc.plot(subjects_dir=subjects_dir, hemi='both', size=300, cortex='0.5')
brain.close()
stc.vertices[1 - idx] = np.array([])
brain = stc.plot(subjects_dir=subjects_dir, hemi=hemi, size=300)
brain.close()
```

## Next Steps


---

*Source: test_brain.py:781 | Complexity: Advanced | Last updated: 2026-05-18*