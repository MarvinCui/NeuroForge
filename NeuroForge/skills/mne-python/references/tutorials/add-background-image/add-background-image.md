# How To: Add Background Image

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test adding background image to a figure.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `cycler`
- `matplotlib`
- `numpy.testing`
- `mne`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.viz`
- `mne.viz.ui_events`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test adding background image to a figure.'

```python
'Test adding background image to a figure.'
```

**Verification:**
```python
assert ax_im.get_aspect() == 'auto'
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert ax.get_aspect() == 1
```

### Step 3: Assign unknown = plt.subplots(...)

```python
f, axs = plt.subplots(1, 2)
```

**Verification:**
```python
assert ax_im_asp.get_aspect() == 'auto'
```

### Step 4: Call plt.close()

```python
plt.close('all')
```

**Verification:**
```python
assert ax.get_aspect() == 'auto'
```

### Step 5: Assign unknown = plt.subplots(...)

```python
f, axs = plt.subplots(1, 2)
```

**Verification:**
```python
assert add_background_image(f, None) is None
```

### Step 6: Assign unknown = rng.randn(...)

```python
x, y = rng.randn(2, 10)
```

### Step 7: Assign im = rng.randn(...)

```python
im = rng.randn(10, 10)
```

### Step 8: Call unknown.scatter()

```python
axs[0].scatter(x, y)
```

### Step 9: Call unknown.scatter()

```python
axs[1].scatter(y, x)
```

### Step 10: Call plt.close()

```python
plt.close('all')
```

### Step 11: Call ax.set_aspect()

```python
ax.set_aspect(1)
```

### Step 12: Assign ax_im = add_background_image(...)

```python
ax_im = add_background_image(f, im)
```

**Verification:**
```python
assert ax_im.get_aspect() == 'auto'
```

### Step 13: Assign ax_im_asp = add_background_image(...)

```python
ax_im_asp = add_background_image(f, im, set_ratios='auto')
```

**Verification:**
```python
assert ax_im_asp.get_aspect() == 'auto'
```


## Complete Example

```python
# Workflow
'Test adding background image to a figure.'
rng = np.random.RandomState(0)
for ii in range(2):
    f, axs = plt.subplots(1, 2)
    x, y = rng.randn(2, 10)
    im = rng.randn(10, 10)
    axs[0].scatter(x, y)
    axs[1].scatter(y, x)
    for ax in axs:
        ax.set_aspect(1)
    if ii == 0:
        ax_im = add_background_image(f, im)
        assert ax_im.get_aspect() == 'auto'
        for ax in axs:
            assert ax.get_aspect() == 1
    else:
        ax_im_asp = add_background_image(f, im, set_ratios='auto')
        assert ax_im_asp.get_aspect() == 'auto'
        for ax in axs:
            assert ax.get_aspect() == 'auto'
    plt.close('all')
f, axs = plt.subplots(1, 2)
assert add_background_image(f, None) is None
plt.close('all')
```

## Next Steps


---

*Source: test_utils.py:95 | Complexity: Advanced | Last updated: 2026-05-18*