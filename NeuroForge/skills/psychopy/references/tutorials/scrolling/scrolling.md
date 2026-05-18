# How To: Scrolling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test scrolling

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `pytest`
- `pandas`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.visual.window`
- `psychopy.visual.form`
- `psychopy.visual.textbox2.textbox2`
- `psychopy.visual.slider`
- `psychopy.tests`
- `shutil`
- `tempfile`
- `numpy`


## Step-by-Step Guide

### Step 1: Assign item = value

```python
item = [{'type': 'slider', 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.7, 'responseColor': 'darkred', 'responseWidth': 0.3, 'font': 'Noto Sans'}]
```

### Step 2: Assign exemplars = value

```python
exemplars = [0, 0.5, 1]
```

### Step 3: Assign tykes = value

```python
tykes = []
```

### Step 4: Assign items = value

```python
items = []
```

### Step 5: Assign survey = Form(...)

```python
survey = Form(self.win, units='height', size=(1, 0.5), fillColor='white', items=items)
```

### Step 6: Call items.append()

```python
items.append(item[0].copy())
```

### Step 7: Assign unknown = value

```python
items[i]['itemText'] = str(i) + items[i]['itemText']
```

### Step 8: Assign survey.scrollbar.rating = case

```python
survey.scrollbar.rating = case
```

### Step 9: Call survey.draw()

```python
survey.draw()
```

### Step 10: Assign filename = value

```python
filename = f'TestForm_scrolling_nq{nItems}_s{case}.png'
```

### Step 11: Call self.win.getMovieFrame.save()

```python
self.win.getMovieFrame(buffer='back').save(Path(utils.TESTS_DATA_PATH) / filename)
```

### Step 12: Call self.win.flip()

```python
self.win.flip()
```


## Complete Example

```python
# Workflow
item = [{'type': 'slider', 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.7, 'responseColor': 'darkred', 'responseWidth': 0.3, 'font': 'Noto Sans'}]
exemplars = [0, 0.5, 1]
tykes = []
for nItems in (1, 3, 10):
    items = []
    for i in range(nItems):
        items.append(item[0].copy())
        items[i]['itemText'] = str(i) + items[i]['itemText']
    survey = Form(self.win, units='height', size=(1, 0.5), fillColor='white', items=items)
    for case in exemplars + tykes:
        survey.scrollbar.rating = case
        survey.draw()
        filename = f'TestForm_scrolling_nq{nItems}_s{case}.png'
        self.win.getMovieFrame(buffer='back').save(Path(utils.TESTS_DATA_PATH) / filename)
        self.win.flip()
```

## Next Steps


---

*Source: test_form.py:272 | Complexity: Advanced | Last updated: 2026-05-18*