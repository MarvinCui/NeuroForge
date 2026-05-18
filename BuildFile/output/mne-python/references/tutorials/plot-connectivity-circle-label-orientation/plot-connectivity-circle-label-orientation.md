# How To: Plot Connectivity Circle Label Orientation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Labels in the 0-90 deg polar range (12-3 o'clock) must not be flipped.

Regression test: previously the condition ``angle_deg >= 270`` missed the
[0, 90) range, incorrectly adding 180 degrees to those labels and setting
ha='right', which caused them to point inward instead of outward.

## Prerequisites

**Required Modules:**
- `matplotlib`
- `numpy`
- `pytest`
- `mne.viz`
- `mne.viz.circle`


## Step-by-Step Guide

### Step 1: "Labels in the 0-90 deg polar range (12-3 o'clock) must not be flipped.\n\n    Regression test: previously the condition ``angle_deg >= 270`` missed the\n    [0, 90) range, incorrectly adding 180 degrees to those labels and setting\n    ha='right', which caused them to point inward instead of outward.\n    "

```python
"Labels in the 0-90 deg polar range (12-3 o'clock) must not be flipped.\n\n    Regression test: previously the condition ``angle_deg >= 270`` missed the\n    [0, 90) range, incorrectly adding 180 degrees to those labels and setting\n    ha='right', which caused them to point inward instead of outward.\n    "
```

**Verification:**
```python
assert len(label_texts) == n_nodes, f'Expected {n_nodes} label texts, found {len(label_texts)}'
```

### Step 2: Assign n_nodes = 9

```python
n_nodes = 9
```

**Verification:**
```python
assert ha == 'left', f"Node '{name}' at {angle:.1f}° (right half) should have ha='left', got '{ha}'"
```

### Step 3: Assign con = np.ones(...)

```python
con = np.ones((n_nodes, n_nodes))
```

**Verification:**
```python
assert ha == 'right', f"Node '{name}' at {angle:.1f}° (left half) should have ha='right', got '{ha}'"
```

### Step 4: Assign unknown = 0

```python
con[::2, ::2] = 0
```

### Step 5: Assign node_names = value

```python
node_names = [f'n{i}' for i in range(n_nodes)]
```

### Step 6: Assign unknown = _plot_connectivity_circle(...)

```python
fig, ax = _plot_connectivity_circle(con, node_names, show=False)
```

### Step 7: Assign texts = value

```python
texts = [c for c in ax.get_children() if isinstance(c, matplotlib.text.Text)]
```

### Step 8: Assign label_texts = value

```python
label_texts = {t.get_text(): t for t in texts if t.get_text() in node_names}
```

### Step 9: Assign angles_deg = np.linspace(...)

```python
angles_deg = np.linspace(0, 360, n_nodes, endpoint=False)
```

**Verification:**
```python
assert len(label_texts) == n_nodes, f'Expected {n_nodes} label texts, found {len(label_texts)}'
```

### Step 10: Assign t = value

```python
t = label_texts[name]
```

### Step 11: Assign ha = t.get_ha(...)

```python
ha = t.get_ha()
```

**Verification:**
```python
assert ha == 'left', f"Node '{name}' at {angle:.1f}° (right half) should have ha='left', got '{ha}'"
```


## Complete Example

```python
# Workflow
"Labels in the 0-90 deg polar range (12-3 o'clock) must not be flipped.\n\n    Regression test: previously the condition ``angle_deg >= 270`` missed the\n    [0, 90) range, incorrectly adding 180 degrees to those labels and setting\n    ha='right', which caused them to point inward instead of outward.\n    "
n_nodes = 9
con = np.ones((n_nodes, n_nodes))
con[::2, ::2] = 0
node_names = [f'n{i}' for i in range(n_nodes)]
fig, ax = _plot_connectivity_circle(con, node_names, show=False)
texts = [c for c in ax.get_children() if isinstance(c, matplotlib.text.Text)]
label_texts = {t.get_text(): t for t in texts if t.get_text() in node_names}
angles_deg = np.linspace(0, 360, n_nodes, endpoint=False)
assert len(label_texts) == n_nodes, f'Expected {n_nodes} label texts, found {len(label_texts)}'
for angle, name in zip(angles_deg, node_names, strict=True):
    t = label_texts[name]
    ha = t.get_ha()
    if angle >= 270 or angle < 90:
        assert ha == 'left', f"Node '{name}' at {angle:.1f}° (right half) should have ha='left', got '{ha}'"
    else:
        assert ha == 'right', f"Node '{name}' at {angle:.1f}° (left half) should have ha='right', got '{ha}'"
```

## Next Steps


---

*Source: test_circle.py:40 | Complexity: Advanced | Last updated: 2026-05-18*