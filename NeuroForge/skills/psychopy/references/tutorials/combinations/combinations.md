# How To: Combinations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that question options interact well

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

### Step 1: '\n        Test that question options interact well\n        '

```python
'\n        Test that question options interact well\n        '
```

### Step 2: Assign exemplars = value

```python
exemplars = {'bigResp': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.3, 'responseColor': 'darkred', 'responseWidth': 0.7, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.3, 'responseColor': 'darkslateblue', 'responseWidth': 0.7, 'font': 'Noto Sans'}], 'bigItem': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.7, 'responseColor': 'darkred', 'responseWidth': 0.3, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.7, 'responseColor': 'darkslateblue', 'responseWidth': 0.3, 'font': 'Noto Sans'}]}
```

### Step 3: Assign tykes = value

```python
tykes = {'bigRespOverflow': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.4, 'responseColor': 'darkred', 'responseWidth': 0.8, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.4, 'responseColor': 'darkslateblue', 'responseWidth': 0.8, 'font': 'Noto Sans'}], 'bigItemOverflow': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.8, 'responseColor': 'darkred', 'responseWidth': 0.4, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.8, 'responseColor': 'darkslateblue', 'responseWidth': 0.4, 'font': 'Noto Sans'}]}
```

### Step 4: Assign cases = exemplars.copy(...)

```python
cases = exemplars.copy()
```

### Step 5: Call cases.update()

```python
cases.update(tykes)
```

### Step 6: Call self.win.flip()

```python
self.win.flip()
```

### Step 7: Assign survey = Form(...)

```python
survey = Form(self.win, units='height', size=(1, 1), fillColor='white', items=case)
```

### Step 8: Call survey.draw()

```python
survey.draw()
```

### Step 9: Assign filename = value

```python
filename = f'test_form_combinations_{thisType}_{name}.png'
```

### Step 10: Call utils.compareScreenshot()

```python
utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
```

### Step 11: Call self.win.flip()

```python
self.win.flip()
```

### Step 12: Assign unknown = thisType

```python
case[i]['type'] = thisType
```


## Complete Example

```python
# Workflow
'\n        Test that question options interact well\n        '
exemplars = {'bigResp': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.3, 'responseColor': 'darkred', 'responseWidth': 0.7, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.3, 'responseColor': 'darkslateblue', 'responseWidth': 0.7, 'font': 'Noto Sans'}], 'bigItem': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.7, 'responseColor': 'darkred', 'responseWidth': 0.3, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.7, 'responseColor': 'darkslateblue', 'responseWidth': 0.3, 'font': 'Noto Sans'}]}
tykes = {'bigRespOverflow': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.4, 'responseColor': 'darkred', 'responseWidth': 0.8, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.4, 'responseColor': 'darkslateblue', 'responseWidth': 0.8, 'font': 'Noto Sans'}], 'bigItemOverflow': [{'index': 1, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'vert', 'itemColor': 'darkslateblue', 'itemWidth': 0.8, 'responseColor': 'darkred', 'responseWidth': 0.4, 'font': 'Noto Sans'}, {'index': 0, 'itemText': 'A PsychoPy zealot knows a smidge of wx but JavaScript is the question', 'options': [1, 'a', 'multiple word'], 'ticks': [1, 2, 3], 'layout': 'horiz', 'itemColor': 'darkred', 'itemWidth': 0.8, 'responseColor': 'darkslateblue', 'responseWidth': 0.4, 'font': 'Noto Sans'}]}
cases = exemplars.copy()
cases.update(tykes)
self.win.flip()
for name, case in cases.items():
    for thisType in self.respTypes:
        for i, q in enumerate(case):
            case[i]['type'] = thisType
        survey = Form(self.win, units='height', size=(1, 1), fillColor='white', items=case)
        survey.draw()
        filename = f'test_form_combinations_{thisType}_{name}.png'
        utils.compareScreenshot(Path(utils.TESTS_DATA_PATH) / filename, self.win, crit=20)
        self.win.flip()
```

## Next Steps


---

*Source: test_form.py:115 | Complexity: Advanced | Last updated: 2026-05-18*