# How To: Importitems

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test importItems

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

### Step 1: Assign wrongFields = value

```python
wrongFields = [{'a': 'What is your gender?', 'b': 0.7, 'c': 'radio', 'd': 0.3, 'e': 'Male, Female, Other', 'f': 'vert', 'g': 'white', 'h': 'white'}]
```

### Step 2: Assign missingHeader = value

```python
missingHeader = [{'qText': 'What is your gender?', 'questionWidth': 0.7, 'type': 'radio', 'responseWidth': 0.3, 'options': 'Other', 'layout': 'vert', 'index': 0, 'questionColor': 'white', 'responseColor': 'white'}]
```

### Step 3: Assign self.survey = Form(...)

```python
self.survey = Form(self.win, items=self.fileName_csv, size=(1.0, 0.3), pos=(0.0, 0.0), autoLog=False)
```

### Step 4: Assign self.survey = Form(...)

```python
self.survey = Form(self.win, items=self.fileName_xlsx, size=(1.0, 0.3), pos=(0.0, 0.0), randomize=False, autoLog=False)
```

### Step 5: Assign self.survey = Form(...)

```python
self.survey = Form(self.win, items=missingHeader, size=(1.0, 0.3), pos=(0.0, 0.0), autoLog=False)
```


## Complete Example

```python
# Workflow
wrongFields = [{'a': 'What is your gender?', 'b': 0.7, 'c': 'radio', 'd': 0.3, 'e': 'Male, Female, Other', 'f': 'vert', 'g': 'white', 'h': 'white'}]
missingHeader = [{'qText': 'What is your gender?', 'questionWidth': 0.7, 'type': 'radio', 'responseWidth': 0.3, 'options': 'Other', 'layout': 'vert', 'index': 0, 'questionColor': 'white', 'responseColor': 'white'}]
with pytest.raises(ValueError):
    self.survey = Form(self.win, items=missingHeader, size=(1.0, 0.3), pos=(0.0, 0.0), autoLog=False)
self.survey = Form(self.win, items=self.fileName_csv, size=(1.0, 0.3), pos=(0.0, 0.0), autoLog=False)
self.survey = Form(self.win, items=self.fileName_xlsx, size=(1.0, 0.3), pos=(0.0, 0.0), randomize=False, autoLog=False)
```

## Next Steps


---

*Source: test_form.py:81 | Complexity: Intermediate | Last updated: 2026-05-18*