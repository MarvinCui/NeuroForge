# How To: Clickable Image

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the ClickableImage class.

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

### Step 1: 'Test the ClickableImage class.'

```python
'Test the ClickableImage class.'
```

**Verification:**
```python
assert_allclose(np.array(clicks), np.array(clk.coords))
```

### Step 2: Assign im = np.random.RandomState.randn(...)

```python
im = np.random.RandomState(0).randn(100, 100)
```

**Verification:**
```python
assert len(clicks) == len(clk.coords)
```

### Step 3: Assign clk = ClickableImage(...)

```python
clk = ClickableImage(im)
```

**Verification:**
```python
assert lt.pos.shape[0] == len(clicks)
```

### Step 4: Assign clicks = value

```python
clicks = [(12, 8), (46, 48), (10, 24)]
```

**Verification:**
```python
assert_allclose(lt.pos[1, 0] / lt.pos[2, 0], clicks[1][0] / float(clicks[2][0]))
```

### Step 5: Call assert_allclose()

```python
assert_allclose(np.array(clicks), np.array(clk.coords))
```

**Verification:**
```python
assert len(clicks) == len(clk.coords)
```

### Step 6: Assign lt = clk.to_layout(...)

```python
lt = clk.to_layout()
```

**Verification:**
```python
assert lt.pos.shape[0] == len(clicks)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(lt.pos[1, 0] / lt.pos[2, 0], clicks[1][0] / float(clicks[2][0]))
```

### Step 8: Call clk.plot_clicks()

```python
clk.plot_clicks()
```

### Step 9: Call plt.close()

```python
plt.close('all')
```

### Step 10: Call _fake_click()

```python
_fake_click(clk.fig, clk.ax, click, xform='data')
```


## Complete Example

```python
# Workflow
'Test the ClickableImage class.'
im = np.random.RandomState(0).randn(100, 100)
clk = ClickableImage(im)
clicks = [(12, 8), (46, 48), (10, 24)]
for click in clicks:
    _fake_click(clk.fig, clk.ax, click, xform='data')
assert_allclose(np.array(clicks), np.array(clk.coords))
assert len(clicks) == len(clk.coords)
lt = clk.to_layout()
assert lt.pos.shape[0] == len(clicks)
assert_allclose(lt.pos[1, 0] / lt.pos[2, 0], clicks[1][0] / float(clicks[2][0]))
clk.plot_clicks()
plt.close('all')
```

## Next Steps


---

*Source: test_utils.py:74 | Complexity: Advanced | Last updated: 2026-05-18*