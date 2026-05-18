# How To: Plot Surf Contours Axis Title

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test nilearn.plotting.surface.plot_surf_contours for axis title.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `tempfile`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.exceptions`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, in_memory_mesh, parcellation
```

## Step-by-Step Guide

### Step 1: 'Test nilearn.plotting.surface.plot_surf_contours for axis title.'

```python
'Test nilearn.plotting.surface.plot_surf_contours for axis title.'
```

**Verification:**
```python
assert display._suptitle is None
```

### Step 2: Assign fig = plot_surf(...)

```python
fig = plot_surf(in_memory_mesh)
```

**Verification:**
```python
assert display.axes[0].get_title() == 'title'
```

### Step 3: Call plot_surf_contours()

```python
plot_surf_contours(in_memory_mesh, parcellation, figure=fig)
```

**Verification:**
```python
assert display._suptitle is None
```

### Step 4: Assign display = plot_surf_contours(...)

```python
display = plot_surf_contours(in_memory_mesh, parcellation, levels=[1, 2], labels=['1', '2'], colors=['r', 'g'], legend=True, title='title', figure=fig)
```

**Verification:**
```python
assert display.axes[0].get_title() == 'title 2'
```

### Step 5: Assign fig = plot_surf(...)

```python
fig = plot_surf(in_memory_mesh, title='title 2')
```

### Step 6: Assign display = plot_surf_contours(...)

```python
display = plot_surf_contours(in_memory_mesh, parcellation, levels=[1, 2], labels=['1', '2'], colors=['r', 'g'], legend=True, figure=fig)
```

**Verification:**
```python
assert display._suptitle is None
```

### Step 7: Call plot_surf_contours()

```python
plot_surf_contours(in_memory_mesh, parcellation, output_file=tmp_file.name)
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, in_memory_mesh, parcellation

# Workflow
'Test nilearn.plotting.surface.plot_surf_contours for axis title.'
fig = plot_surf(in_memory_mesh)
plot_surf_contours(in_memory_mesh, parcellation, figure=fig)
display = plot_surf_contours(in_memory_mesh, parcellation, levels=[1, 2], labels=['1', '2'], colors=['r', 'g'], legend=True, title='title', figure=fig)
assert display._suptitle is None
assert display.axes[0].get_title() == 'title'
fig = plot_surf(in_memory_mesh, title='title 2')
display = plot_surf_contours(in_memory_mesh, parcellation, levels=[1, 2], labels=['1', '2'], colors=['r', 'g'], legend=True, figure=fig)
assert display._suptitle is None
assert display.axes[0].get_title() == 'title 2'
with tempfile.NamedTemporaryFile() as tmp_file:
    plot_surf_contours(in_memory_mesh, parcellation, output_file=tmp_file.name)
```

## Next Steps


---

*Source: test_surf_plotting.py:513 | Complexity: Intermediate | Last updated: 2026-05-18*