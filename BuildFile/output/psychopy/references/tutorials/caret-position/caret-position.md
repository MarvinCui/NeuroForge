# How To: Caret Position

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test caret position

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `psychopy`
- `psychopy.alerts`
- `psychopy.alerts._errorHandler`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.visual`
- `psychopy.visual`
- `psychopy.tools.fontmanager`
- `pytest`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: Assign indices = value

```python
indices = (4, 30, 64)
```

**Verification:**
```python
assert all(np.isclose(caretVerts[0], charVerts[2], 1)), f"Textbox caret at index {i} didn't align with bottom right corner of matching char when:\nanchor={anchor}, alignment={align}, flipHoriz={flipHoriz}, flipVert={flipVert}.\nCaret vertices were:\n{caretVerts}\nChar verts were \n{charVerts}\n"
```

### Step 2: Assign anchalign = value

```python
anchalign = ('center', 'top-center', 'bottom-center', 'center-left', 'center-right', 'top-left', 'top-right', 'bottom-left', 'bottom-right')
```

### Step 3: Assign textbox = TextBox2(...)

```python
textbox = TextBox2(self.win, text='A PsychoPy zealot knows a smidge of wx, but JavaScript is the \nquestion.', size=(128, 64), pos=(0, 0), units='pix', anchor=anchor, alignment=align, flipHoriz=flipHoriz, flipVert=flipVert)
```

### Step 4: Assign textbox.caret.index = i

```python
textbox.caret.index = i
```

### Step 5: Call textbox.draw()

```python
textbox.draw()
```

### Step 6: Call textbox.caret.draw()

```python
textbox.caret.draw()
```

### Step 7: Assign caretVerts = value

```python
caretVerts = textbox.caret.vertices
```

### Step 8: Assign charVerts = value

```python
charVerts = textbox._vertices.pix[range((i - 1) * 4, (i - 1) * 4 + 4)]
```

**Verification:**
```python
assert all(np.isclose(caretVerts[0], charVerts[2], 1)), f"Textbox caret at index {i} didn't align with bottom right corner of matching char when:\nanchor={anchor}, alignment={align}, flipHoriz={flipHoriz}, flipVert={flipVert}.\nCaret vertices were:\n{caretVerts}\nChar verts were \n{charVerts}\n"
```


## Complete Example

```python
# Workflow
indices = (4, 30, 64)
anchalign = ('center', 'top-center', 'bottom-center', 'center-left', 'center-right', 'top-left', 'top-right', 'bottom-left', 'bottom-right')
for anchor in anchalign:
    for align in anchalign:
        for flipHoriz in (True, False):
            for flipVert in (True, False):
                textbox = TextBox2(self.win, text='A PsychoPy zealot knows a smidge of wx, but JavaScript is the \nquestion.', size=(128, 64), pos=(0, 0), units='pix', anchor=anchor, alignment=align, flipHoriz=flipHoriz, flipVert=flipVert)
                for i in indices:
                    textbox.caret.index = i
                    textbox.draw()
                    textbox.caret.draw()
                    caretVerts = textbox.caret.vertices
                    charVerts = textbox._vertices.pix[range((i - 1) * 4, (i - 1) * 4 + 4)]
                    assert all(np.isclose(caretVerts[0], charVerts[2], 1)), f"Textbox caret at index {i} didn't align with bottom right corner of matching char when:\nanchor={anchor}, alignment={align}, flipHoriz={flipHoriz}, flipVert={flipVert}.\nCaret vertices were:\n{caretVerts}\nChar verts were \n{charVerts}\n"
```

## Next Steps


---

*Source: test_textbox.py:344 | Complexity: Advanced | Last updated: 2026-05-18*