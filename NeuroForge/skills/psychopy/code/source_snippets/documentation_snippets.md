# psychopy Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Contributing to the PsychoPy Test Suite #3

- Kind: `documentation`
- Source: `references/documentation/other/readme.md`
- Note: Documentation code block extracted for implementation use.

```python
# Set the rectangle's fill color
rect.colorSpace = 'rgb'
rect.fillColor = (1, -1, -1)
# Check that the rgb value of its fill color is consistent with what we set 
assert rect._fillColor == colors.Color('red'), f"Was expecting rect._fillColor to have an rgb value of '(1, -1, -1)', but instead it was '{rect._fillColor.rgb}'"
```

## 2. Contributing to the PsychoPy Test Suite #1

- Kind: `documentation`
- Source: `references/documentation/other/readme.md`
- Note: Documentation code block extracted for implementation use.

```python
from psychopy import visual  # used to draw stimuli

def test_rect():
    # Test that we can create a window and a rectangle without error
    win = visual.Window()
    rect = visual.Rect(win)
    # Check that they draw without error
    rect.draw()
    win.flip()
    # End test
    win.close()
```

## 3. Contributing to the PsychoPy Test Suite #2

- Kind: `documentation`
- Source: `references/documentation/other/readme.md`
- Note: Documentation code block extracted for implementation use.

```python
assert 2 < 1, "2 is not less than 1"
```
